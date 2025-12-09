---
title: "Blog 3"
date: "2025-09-08"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

### How to build highly available Kubernetes applications with Amazon EKS Auto Mode

**Bởi Doruk Ozturk, Nikita Ravi Shetty, và Divya Gupta** | ngày 09 tháng 9 năm 2025

Khi các tổ chức mở rộng triển khai Kubernetes, nhiều tổ chức phải đối mặt với những thách thức vận hành quan trọng. Hãy xem xét cách các đội ngũ DevOps dành hàng giờ để lập kế hoạch và thực hiện nâng cấp cluster, quản lý các tiện ích mở rộng (add-on) và đảm bảo các bản vá bảo mật được áp dụng một cách nhất quán. Có nhu cầu rõ ràng về khả năng quản lý vòng đời cluster một cách tự động và đáng tin cậy, khi các đội ngũ vẫn đang phải vật lộn để duy trì cấu hình cluster và tư thế bảo mật nhất quán trên các môi trường khác nhau. [Amazon Elastic Kubernetes Service (Amazon EKS) Auto Mode](https://aws.amazon.com/eks/auto-mode/) giải quyết những thách thức này bằng cách tự động hóa việc cập nhật control plane, tối ưu hóa quản lý các tiện ích mở rộng và đảm bảo các cluster luôn duy trì theo các best practice hiện tại.

Bài viết này đi sâu vào khả năng của EKS Auto Mode, thử nghiệm nó trong một loạt các tình huống thách thức như mô phỏng sự cố, tái sử dụng node và nâng cấp cluster — tất cả đều duy trì lưu lượng dịch vụ không bị gián đoạn. Tài liệu hướng dẫn này đi sâu vào các chiến lược để đạt được tính khả dụng cao trong bối cảnh tính chất động của EKS Auto Mode bằng cách sử dụng các tính năng của Kubernetes để tối đa hóa thời gian hoạt động. Mục tiêu là cung cấp một hướng dẫn toàn diện về cách khai thác tiềm năng của EKS Auto Mode, đảm bảo dịch vụ của bạn luôn mạnh mẽ và linh hoạt trong các môi trường đòi hỏi khắt khe. Mặc dù có rất nhiều tài liệu chuyên sâu về độ tin cậy trong hệ sinh thái container nói chung, nhưng bài viết này tập trung vào những cân nhắc cụ thể khi vận hành workload đáng tin cậy trong môi trường EKS Auto Mode.

# Tổng quan về giải pháp

Trước khi đi sâu vào các chi tiết cụ thể của Amazon EKS và [tính năng Auto Mode](https://aws.amazon.com/blogs/containers/under-the-hood-amazon-eks-auto-mode/), bạn cần hiểu rõ các khái niệm cốt lõi trong Kubernetes — những yếu tố đóng vai trò then chốt trong việc tối đa hóa thời gian uptime của dịch vụ trong các sự kiện khác nhau của cluster. Những thành phần nền tảng này tạo nên nền móng cho các kiến trúc ứng dụng bền vững trong môi trường Kubernetes, bất kể nhà cung cấp đám mây cụ thể hoặc chế độ quản lý nào. Nắm vững các khái niệm này giúp bạn sử dụng EKS Auto Mode một cách hiệu quả và xây dựng các hệ thống có độ khả dụng cao có thể chống chịu được nhiều thách thức vận hành khác nhau. Trong phần này, chúng ta sẽ khám phá các tính năng thiết yếu của Kubernetes, những tính năng đóng vai trò trọng yếu trong việc duy trì tính liên tục của dịch vụ (service continuity) trong cả các sự kiện được lên kế hoạch và không được lên kế hoạch.

[Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) giới hạn số lượng gián đoạn đồng thời mà ứng dụng có thể trải qua, cho phép duy trì độ khả dụng cao. PDB bảo vệ khi các node bị drain để bảo trì hoặc mở rộng quy mô, đảm bảo rằng phần lớn các bản sao của một service không bị dừng cùng lúc.

```yaml
spec:
  minAvailable: 80%
  selector:
    matchLabels:
      app.kubernetes.io/name: app-2048
````

[Pod Readiness Gates](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.12/deploy/pod_readiness_gate/) là yếu tố thiết yếu để đạt được triển khai không gián đoạn (zero-downtime deployments) khi sử dụng AWS load balancer (máy cân bằng tải). Các pod mới thường đăng ký với target group (nhóm mục tiêu) chậm hơn so với quá trình rollout deployment, vì vậy có thể xảy ra gián đoạn dịch vụ khi chỉ còn các target ở trạng thái Initial hoặc Draining. Việc triển khai Pod Readiness Gates ở cấp namespace có nghĩa là các pod sẽ không bị chấm dứt (terminate) cho đến khi các pod thay thế được xác nhận là Healthy trong [Application Load Balancers (ALBs)](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) hoặc [Network Load Balancers (NLBs)](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html), do đó loại bỏ các khoảng trống trong quá trình triển khai.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: game-2048
  labels:
    [eks.amazonaws.com/pod-readiness-gate-inject](https://eks.amazonaws.com/pod-readiness-gate-inject): enabled
```

[Deregistration Delay Timeout](https://www.google.com/search?q=https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html%23target-group-attributes) là khoảng thời gian giữa khi một target được đánh dấu để loại bỏ (removal) và khi nó ngừng nhận các yêu cầu mới. Điều này cho phép các request đang xử lý được hoàn tất một cách trơn tru trước khi bị chấm dứt, và thường được sử dụng với load balancer. Giá trị mặc định là 300 giây. Thiết lập này giúp giảm thiểu gián đoạn cho người dùng và đảm bảo quá trình chuyển đổi mượt mà hơn khi bạn loại bỏ các target khỏi target group.

```yaml
annotations:
  alb.ingress.kubernetes.io/scheme: internet-facing
  alb.ingress.kubernetes.io/target-type: ip
  alb.ingress.kubernetes.io/target-group-attributes: deregistration_delay.timeout_seconds=30
```

[Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) cung cấp khả năng kiểm soát quan trọng đối với việc phân phối pod qua các miền lỗi (failure domains) (như node, [Availability Zones (AZs)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/), và các vùng AWS Region), đóng vai trò như một cơ chế mạnh mẽ để đảm bảo tính khả dụng cao bằng cách ngăn chặn việc tập trung workload tại các điểm lỗi đơn lẻ. `maxSkew: 1` có nghĩa là cấu hình này đảm bảo không có zone hoặc node nào có nhiều hơn một pod dư thừa so với các zone khác. Điều này thúc đẩy phân phối tải công việc tối ưu đồng thời duy trì tính linh hoạt trong lịch trình với `ScheduleAnyway`.

```yaml
topologySpreadConstraints:
  - maxSkew: 1
    whenUnsatisfiable: ScheduleAnyway
    topologyKey: topology.kubernetes.io/zone
    labelSelector:
      matchLabels:
        app.kubernetes.io/name: app-2048
  - maxSkew: 1
    topologyKey: kubernetes.io/hostname
    whenUnsatisfiable: ScheduleAnyway
    labelSelector:
      matchLabels:
        app.kubernetes.io/name: app-2048
```

[Termination Grace Period](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/) là khoảng thời gian dành cho một pod để tắt một cách nhẹ nhàng trước khi bị buộc chấm dứt (giá trị mặc định là 30 giây). Điều này cho phép ứng dụng dọn dẹp tài nguyên và đóng kết nối trước khi bị ngừng hoạt động.

```yaml
terminationGracePeriodSeconds: 60
```

[SIGTERM Handling](https://www.google.com/search?q=https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/%23pod-termination) là cơ chế thực thi ở cấp ứng dụng để xử lý một cách trơn tru các tín hiệu tắt máy từ Kubernetes. Điều này cho phép dọn dẹp tài nguyên một cách đúng đắn, lưu trạng thái và đóng kết nối trước khi kết thúc quá trình.

```yaml
lifecycle:
  preStop:
    exec:
      command: ["/bin/sh", "-c", "sleep 10"]
```

[Liveness probes](https://www.google.com/search?q=https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/%23define-a-liveness-command) kiểm tra xem container có đang hoạt động bình thường hay không và khởi động lại nó nếu các kiểm tra thất bại, trong khi [readiness probes](https://www.google.com/search?q=https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/%23define-readiness-probes) xác định xem container có sẵn sàng để xử lý traffic hay không và loại bỏ nó khỏi load balancer nếu chưa sẵn sàng. Hai loại kiểm tra này hoạt động cùng nhau trong Kubernetes để đảm bảo sức khỏe của ứng dụng và quản lý lưu lượng truy cập một cách chính xác.

```yaml
readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 5
  timeoutSeconds: 2
  successThreshold: 1
  failureThreshold: 3
livenessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 15
  periodSeconds: 10
  timeoutSeconds: 2
  successThreshold: 1
  failureThreshold: 3
```

Ứng dụng mẫu triển khai một chiến lược khả năng phục hồi toàn diện với nhiều cơ chế bảo vệ. Pod Disruption Budget duy trì độ khả dụng tối thiểu 80% trong quá trình bảo trì, và Pod Readiness Gates (thông qua `elbv2.k8s.aws/pod-readiness-gate-inject: enabled`) ngăn chặn việc kết thúc sớm, Deregistration delay được tối ưu trước 30 giây, và Phân phối pod cân bằng giữa các AZ và node thông qua topology constraints (`maxSkew=1`). Lifecycle management mượt mà thông qua chuỗi tắt 60 giây gồm 10 giây preStop và 50 giây xử lý SIGTERM. Ngoài ra, nó được bổ sung bằng dual health monitoring sử dụng readiness probes cho quản lý lưu lượng cùng với liveness probes xử lý kiểm tra sức khỏe container để duy trì tính ổn định của hệ thống. Kiến trúc này đảm bảo tính sẵn sàng nhất quán, phân phối tải thông minh và chuyển đổi không gián đoạn trong suốt vòng đời ứng dụng.

# Test scenarios

Để minh họa, nhóm tác giả đã chọn [Amazon EKS Elastic Load Balancer example](https://docs.aws.amazon.com/eks/latest/userguide/auto-elb-example.html) làm workload tham chiếu. Ứng dụng cụ thể không quá quan trọng trong trường hợp này, bởi mục đích chính là trình bày các nguyên tắc phổ quát có thể áp dụng cho mọi workload Kubernetes.

> *Hình 1: Các kịch bản sự cố khác nhau được hiển thị trên biểu đồ uptime được theo dõi bằng công cụ Uptime Kuma*

Để phục vụ cho bài demo, nhóm sử dụng công cụ giám sát bên thứ ba Uptime Kuma.

Bạn có thể mô phỏng biểu đồ và các ví dụ tiếp theo bằng cách chạy công cụ [uptime-kuma](https://github.com/louislam/uptime-kuma) trong container Docker hoặc cài đặt cục bộ theo hướng dẫn trong GitHub, và cấu hình nó để giám sát ALB của bạn. Cách này cho phép bạn theo dõi lưu lượng và độ khả dụng của các ứng dụng được tiếp xúc thông qua ALB.

## Pod fail scenario

Khi các pod riêng lẻ gặp lỗi bất ngờ, Kubernetes phải nhanh chóng khôi phục khả năng cung cấp dịch vụ. Kiểm tra này chủ động kết thúc một pod duy nhất để xác minh khả năng tái tạo tự động (auto recreation) của controller, xác nhận hiệu quả của readiness probe và đo lường thời gian khôi phục. Mục đích là đánh giá mức độ duy trì tính liên tục của dịch vụ trong ứng dụng khi gặp các lỗi microservice phổ biến.

Sau khi xóa một pod, Kubernetes ngay lập tức phát hiện việc chấm dứt pod. Một pod mới được lên lịch và tạo ra ngay lập tức để thay thế pod đã bị kết thúc. Readiness probe đảm bảo rằng pod mới hoạt động đầy đủ trước khi nhận traffic. PDB đảm bảo rằng số lượng pod tối thiểu vẫn khả dụng trong quá trình này. Do đó, tính liên tục của dịch vụ được duy trì với sự gián đoạn tối thiểu. Hình minh họa trước đó giúp xác minh rằng hệ thống hoạt động như mong đợi và duy trì mức độ khả dụng mong muốn.

## Node fail scenario

Các bài kiểm tra lỗi node mô phỏng sự cố ngừng hoạt động hoàn toàn của máy chủ bằng cách cách ly và xả tải các nút. Điều này xác minh cơ chế tái lập lịch pod (pod rescheduling), đánh giá cách các topology spread constraints tái phân phối workload và đo lường hiệu quả của PDB trong việc duy trì tính khả dụng tối thiểu. Bài kiểm tra này cho thấy liệu các ứng dụng có chịu được sự cố phần cứng mà không gây gián đoạn dịch vụ hay không.

Sau khi xóa một node, Kubernetes đánh dấu node đó là không thể lên lịch (cordon) và các pod hiện có được di chuyển an toàn khỏi node (drain). Các pod được tự động lên lịch lại sang các node healthy dựa trên tài nguyên khả dụng, các Topology Spread Constraints và yêu cầu PDB về khả năng sẵn sàng tối thiểu. Hình minh họa trước đó cho thấy tính liên tục của dịch vụ trong quá trình mô phỏng sự cố node, chứng minh khả năng chống chịu của hệ thống trước các sự cố phần cứng.

## AZ fail scenario

Mô phỏng sự cố ngừng hoạt động toàn bộ Availability Zone (AZ) cho phép chúng ta xác minh khả năng chịu lỗi của kiến trúc đa AZ (multi-AZ). Các thử nghiệm này xác nhận rằng cấu hình topologie phân phối workload một cách chính xác giữa các zone và ứng dụng có thể hoạt động với công suất giảm khi toàn bộ AZ không khả dụng. Điều này rất quan trọng cho kế hoạch khôi phục thảm họa khu vực. Để mô phỏng điều này, nhóm tác giả xóa tất cả các node khỏi một AZ duy nhất để xác minh xem các node bị drain một cách an toàn và các pod trong zone đó trở nên unhealthy hay không. Kubernetes sẽ tái phân bổ chúng vào các healthy node dựa theo topology spread constraints, và các node mới sẽ được khởi động theo yêu cầu của workload và tình trạng của vùng AZ được khôi phục. Hình minh họa trước đó cho thấy dịch vụ tiếp tục hoạt động với công suất giảm nhưng vẫn duy trì khả năng hoạt động, từ đó xác nhận hiệu quả của kế hoạch phục hồi thảm họa (disaster recovery) và chiến lược dự phòng vùng (zone redundancy strategy).

## Cluster version upgrade scenario

Bài kiểm tra khả năng phục hồi khi nâng cấp xác nhận khả năng tương thích của ứng dụng giữa các phiên bản Kubernetes, và đo thời gian downtime trong quá trình chuyển đổi control plane và data plane. Bài kiểm tra xác minh rằng chiến lược triển khai có thể điều chỉnh rolling upgrade cho các node trong khi vẫn tuân thủ PDBs và Node Disruption Budgets (NDBs).

Quá trình nâng cấp được khởi tạo từ AWS Management Console. Hình minh họa bên dưới thể hiện cách mà ứng dụng vẫn khả dụng bằng cách ping URL của ALB mỗi 20 giây trong suốt quá trình nâng cấp cả control plane lẫn worker node.

> *Hình 2: Nâng cấp cluster*

## Karpenter node disruption

Đánh giá Karpenter node disruption triển khai một bản cấu hình manifest tùy chỉnh cho Nodepool, thay thế các node Kubernetes theo chu kỳ 5 phút như minh họa bên dưới, nhằm tạo ra sự biến động có kiểm soát của cơ sở hạ tầng có kiểm soát để đánh giá một cách có hệ thống tính khả dụng của ứng dụng.

Hình 1 trong bài thể hiện các chỉ số về tính khả dụng của dịch vụ trong giai đoạn biến động cơ sở hạ tầng được kiểm soát, chứng minh rằng ứng dụng vẫn ổn định ngay cả khi thay thế node thường xuyên.

```yaml
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  name: expire-quickly
spec:
  disruption:
    budgets:
      - nodes: 10%
        reasons:
          - "Empty"
          - "Drifted"
    consolidateAfter: 60s
    consolidationPolicy: WhenEmptyOrUnderutilized
  template:
    metadata:
    spec:
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      requirements:
        - key: "[eks.amazonaws.com/instance-category](https://eks.amazonaws.com/instance-category)"
          operator: In
          values: ["c", "m", "r"]
        - key: "topology.kubernetes.io/zone"
          operator: In
          values: ["us-west-2a", "us-west-2b", "us-west-2c"]
        - key: "kubernetes.io/arch"
          operator: In
          values: ["amd64"]
        - key: "kubernetes.io/os"
          operator: In
          values: ["linux"]
        - key: "karpenter.sh/capacity-type"
          operator: In
          values: ["on-demand"]
      taints:
        - key: recycle
          value: "true"
          effect: "NoSchedule"
      expireAfter: 5m
  limits:
    cpu: "1000"
    memory: 1000Gi
```

Để tổng hợp các kịch bản thử nghiệm trên, các tính năng của EKS Auto Mode thể hiện sự đánh đổi hợp lý giữa khả năng phục hồi của ứng dụng (application resiliency) và tối ưu chi phí (cost optimization).

Về khả năng phục hồi, EKS Auto Mode duy trì độ khả dụng cao của ứng dụng bằng cách tự động thêm hoặc loại bỏ node tùy theo nhu cầu ứng dụng. Nó thay thế các node trong khung thời gian được cấp (tối đa 21 ngày) để đảm bảo rằng các node luôn chạy bản vá và cập nhật bảo mật mới nhất. Trong quá trình nâng cấp Kubernetes, EKS Auto Mode xử lý thông minh và tuân thủ cấu hình PDB.

Về tối ưu chi phí, EKS Auto Mode chủ động giám sát và chấm dứt các instance không được sử dụng hoặc ít được sử dụng, đảm bảo rằng tổ chức không lãng phí tài nguyên tính toán nhàn rỗi. Ngoài ra, nó liên tục đánh giá để hợp nhất workload vào các node phù hợp, và cân bằng chi phí tính toán bằng cách duy trì tuân thủ nghiêm ngặt các yêu cầu NodePool đối với loại instance.

# Tổng kết

Việc kiểm thử toàn diện Amazon EKS Auto Mode qua các kịch bản lỗi và nâng cấp đã chứng minh khả năng phục hồi (resilience) của cluster khi được cấu hình đúng theo các Kubernetes best practice để đạt được độ khả dụng cao (high availability). Việc triển khai các tính năng như Pod Disruption Budgets, Pod Readiness Gates, Topology Spread Constraints và quản lý vòng đời pod hiệu quả đã giúp ứng dụng đạt được thời gian hoạt động ổn định ngay cả khi xảy ra lỗi pod, gián đoạn node, mô phỏng sự cố AZ, và nâng cấp cluster. Kết quả này nhấn mạnh rằng mặc dù EKS Auto Mode giúp đơn giản hóa việc quản lý cluster, chính việc triển khai cẩn thận các tính năng gốc của Kubernetes mới thực sự mang lại khả năng khả dụng cao. Hơn nữa, các nguyên tắc cơ bản và thực hành đã được thiết lập trong các tài liệu AWS — là tài liệu “[Vận hành các workload có khả năng phục hồi trên Amazon EKS](https://aws.amazon.com/blogs/containers/operating-resilient-workloads-on-amazon-eks/)” và “[Best practice về độ tin cậy cho Amazon EKS](https://docs.aws.amazon.com/eks/latest/best-practices/reliability.html)” — vẫn liên quan và có thể áp dụng. Những tài liệu này đóng vai trò như kiến thức nền tảng thiết yếu, bổ sung cho trọng tâm chuyên sâu được mô tả trong bài viết này.

Đối với các nhóm muốn tối đa hóa độ tin cậy của EKS cluster, chúng tôi khuyến nghị triển khai PDBs một cách toàn diện, sử dụng Pod Readiness Gates kết hợp với AWS load balancer, thiết kế ứng dụng có shutdown handling và kiểm tra tình trạng đúng cách, đồng thời sử dụng Karpenter để quản lý node hiệu quả. Việc kết hợp tính tự động của EKS Auto Mode với các tính năng nâng cao của Kubernetes này cho phép các tổ chức đạt được một môi trường Kubernetes có độ khả dụng cao và dễ quản lý, đáp ứng nhu cầu của các ứng dụng hiện đại theo kiến trúc cloud-native. Để tìm hiểu thêm về EKS Auto Mode, hãy tham khảo [workshop](https://aws.amazon.com/blogs/containers/introducing-the-amazon-eks-auto-mode-workshop/).

# Về tác giả

**Doruk Ozturk** là Senior Containers Specialist Solutions Architect tại Amazon Web Services, chuyên về các ngành Chăm sóc sức khỏe (Healthcare) và Khoa học đời sống (Life Sciences). Với hơn mười năm kinh nghiệm trong lĩnh vực kỹ thuật phần mềm, anh cung cấp hướng dẫn kỹ thuật cho khách hàng trong việc tận dụng công nghệ container của AWS. Doruk hiện sinh sống tại New York City, thích du lịch cùng vợ, chơi trống với các ban nhạc địa phương, và chơi bi-a giải trí trong thời gian rảnh.

[Divya Gupta](https://www.linkedin.com/in/divya-gupta-66981a40) là Associate Specialist Solutions Architect tại AWS.

[Nikita Ravi Shetty](https://www.linkedin.com/in/nikitarshetty) là Associate Solutions Architect tại AWS, tập trung vào lĩnh vực containers. Cô hỗ trợ các khách hàng thuộc ngành viễn thông toàn cầu và bán lẻ/hàng tiêu dùng trong việc di cư và hiện đại hóa các ứng dụng trên AWS. Ngoài công việc, cô yêu thích xem các chương trình trực tuyến, khám phá ẩm thực đa dạng, và kết nối với bạn bè và gia đình.

```
```