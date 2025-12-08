---
title: "Blog 2"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
### Deploy Amazon Timestream for InfluxDB instances with AWS CloudFormation and HashiCorp Terraform

**Bởi Trevor Bonas** | Ngày 9 tháng 9, 2025 | tại [Advanced (300)](https://aws.amazon.com/blogs/database/category/learning-levels/advanced-300/), [Amazon Timestream](https://aws.amazon.com/blogs/database/category/database/amazon-timestream/), [Technical How-to](https://aws.amazon.com/blogs/database/category/post-types/technical-how-to/)

[Amazon Timestream for InfluxDB](https://docs.aws.amazon.com/timestream/latest/developerguide/timestream-for-influxdb.html) là một dịch vụ cơ sở dữ liệu chuỗi thời gian (managed time series database engine) mà bạn có thể sử dụng để chạy InfluxDB databases trên AWS cho các ứng dụng time series theo thời gian thực bằng cách dùng open source APIs. Nếu bạn đang tìm kiếm một hạ tầng Timestream for InfluxDB có tính linh hoạt, khả năng mở rộng cao, [AWS CloudFormation](https://aws.amazon.com/cloudformation/) và [HashiCorp Terraform](https://www.terraform.io/) cung cấp các công cụ đáp ứng nhu cầu đó. Giải pháp này có thể thích ứng động với các yêu cầu thay đổi theo Region và khối lượng công việc phát triển.

Trong bài viết này, chúng tôi sẽ hướng dẫn bạn cách sử dụng AWS CloudFormation và Terraform để tự động hóa việc triển khai và gỡ bỏ (teardown) Timestream for InfluxDB instance.

# Tổng quan giải pháp

Đối với trường hợp sử dụng ví dụ của chúng tôi, nhiều cảm biến sẽ tạo ra dữ liệu chuỗi thời gian trong một giải vô địch đua xe thể thao, với các chặng đua diễn ra ở nhiều quốc gia trên toàn thế giới. Dữ liệu chuỗi thời gian này bao gồm nhiệt độ đường đua, thời gian hoàn thành vòng đua, vị trí tay đua và tốc độ xe. Sự kiện toàn cầu này yêu cầu các phiên bản Timestream for InfluxDB ở các Region (khu vực AWS) khác nhau trên toàn cầu để lưu trữ dữ liệu này một cách hiệu quả.

Trong suốt các cuộc đua, dữ liệu chuỗi thời gian theo dõi xe, tay đua, khoảng cách, vòng đua và thời tiết được gửi đến một instance Timestream for InfluxDB. Các instance này cần được đặt gần sự kiện nhất có thể nhằm cung cấp thông tin chính xác và cập nhật nhất về các cuộc đua, đồng thời đáp ứng các yêu cầu về chủ quyền dữ liệu ở các quốc gia khác nhau.

Timestream for InfluxDB chấp nhận dữ liệu theo [line protocol (định dạng giao thức dòng)](https://docs.influxdata.com/influxdb/v2/reference/syntax/line-protocol/). Dữ liệu theo giao thức dòng bao gồm các thành phần sau, theo thứ tự:

* Một chỉ số đo lường (một chỉ số cho biết điều gì đang được đo lường)
* Một tập tag (tập các thuộc tính metadata)
* Một tập field (tập giá trị)
* Một Unix timestamp

Dưới đây là một ví dụ về một điểm giao thức dòng giả định cho một trình điều khiển trong một sự kiện đua xe:

```text
circuit_paul_ricard,driver_number=”21” rpm=10987,speed=309,throttle=82 1728486666
````

Đoạn mã chứa các tham số sau:

  * `circuit_paul_ricard` là measurement. Trong trường hợp này, đây là tên của một đường đua ở Pháp.
  * `driver_number` là tag có số định danh duy nhất của tay đua hiện tại của xe.
  * `rpm` là field chứa số vòng quay mỗi phút của động cơ xe.
  * `speed` là field chứa tốc độ hiện tại của xe tính bằng km/h.
  * `throttle` là field chứa phần trăm công suất động cơ xe đang được sử dụng.
  * Thành phần cuối cùng là dấu thời gian Unix khi điểm dữ liệu này được sinh ra.

Để cung cấp dữ liệu mới nhất, instance Timestream cho InfluxDB phải được triển khai trong Region gần nhất với nơi diễn ra cuộc đua. Trong suốt cuộc đua, instance này đồng thời nhận dữ liệu chuỗi thời gian từ nhiều khía cạnh của cuộc thi, bao gồm dữ liệu telemetry, thống kê của tay đua và điều kiện môi trường.

Sơ đồ sau đây minh họa một ví dụ về instance Timestream for InfluxDB trong Region Châu Âu (Paris) (eu-west-3) nhận dữ liệu giao thức dòng trong sự kiện đua xe tại Circuit Paul Ricard. Dữ liệu được tạo ra bởi các xe đua và truyền qua hệ thống giám sát và hạ tầng trên đường đua, nơi thu thập và chuyển tiếp thông tin giám sát từ xa.

\![Sơ đồ minh họa instance Timestream for InfluxDB nhận dữ liệu tại Circuit Paul Ricard]

Các tài nguyên được sử dụng trong kịch bản này gồm:

  * Internet gateway, public subnet và route table cung cấp quyền truy cập internet công khai cho database instance, cho phép dữ liệu giám sát đầu vào được ghi vào. Nếu bạn triển khai instance cơ sở dữ liệu trong public subnet, hãy đảm bảo tuân thủ các [best practice về bảo mật](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html).
  * Với một [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (Amazon EC2) instance, dữ liệu được truyền qua hệ thống giám sát theo dõi được sử dụng cho phân tích và trực quan hóa thời gian thực.
  * Một [Amazon Simple Storage Service](https://aws.amazon.com/s3) (Amazon S3) lưu trữ nhật ký cơ sở dữ liệu.

Giải pháp trong bài viết này khác với kịch bản này. Giải pháp trong bài viết này đặt instance cơ sở dữ liệu trong một private subnet và chỉ cấp quyền truy cập cho EC2 instance, tăng cường bảo mật.

Dưới đây là một ví dụ về bảng điều khiển [Grafana](https://grafana.com/docs/grafana/latest/) hiển thị dữ liệu đua xe từ hai cuộc đua, được nhập vào các Timestream for InfluxDB instances riêng biệt trong các Region khác nhau. Dữ liệu bao gồm vị trí của các tay đua, tốc độ và nhiệt độ đường đua.

\![Ví dụ bảng điều khiển Grafana hiển thị dữ liệu đua xe]

Khi cuộc đua kết thúc và một cuộc đua khác bắt đầu ở một quốc gia và Region khác, bạn có thể thực hiện một trong các hành động sau với instance gốc tùy thuộc vào vị trí của cuộc đua tiếp theo:

  * Nếu cuộc đua tiếp theo nằm gần về mặt địa lý với nơi diễn ra cuộc đua cuối cùng, bạn có thể xóa Timestream for InfluxDB instance trên Region đó (để xóa dữ liệu của nó) và tạo lại nó trong cùng Region cho cuộc đua tiếp theo.
  * Nếu cuộc đua tiếp theo gần với một Region khác, bạn có thể xóa Timestream for InfluxDB instance trên Region đó và tạo lại nó trong Region mới cho cuộc đua tiếp theo.

Trong cả hai trường hợp, bạn phải quyết định xem có muốn chuyển dữ liệu hiện có (từ các cuộc đua trước) sang instance mới hay không. Bạn có thể sử dụng [Influx CLI](https://docs.influxdata.com/influxdb/v2/admin/backup-restore/) hoặc [Influx migration script](https://docs.aws.amazon.com/timestream/latest/developerguide/timestream-for-influx-getting-started-migrating-data.html), có thể lưu trữ dữ liệu sao lưu trên Amazon S3, để di chuyển dữ liệu giữa các instance.

Trong các phần tiếp theo, chúng tôi sẽ hướng dẫn bạn cách thực hiện điều này bằng cách sử dụng AWS CloudFormation hoặc Terraform.

Giải pháp trong bài viết này sử dụng các tài nguyên AWS sau:

  * Một [instance](https://aws.amazon.com/ec2/instance-types/) EC2
  * Một [stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html) CloudFormation
  * [Amazon Virtual Private Cloud](https://aws.amazon.com/vpc/) (Amazon VPC)
  * Hai VPC [security group](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
  * Hai VPC [subnet](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html)
  * Một Timestream for InfluxDB [instance](https://www.google.com/search?q=https://docs.aws.amazon.com/timestream/latest/developerguide/timestream-for-influxdb.html%23timestream-for-influx-db-instances)

Bạn sẽ phải trả phí cho các tài nguyên AWS được sử dụng trong giải pháp này. Chạy giải pháp này với các giá trị cấu hình mặc định trong Region US West (Oregon) trong 1 giờ có chi phí khoảng $0.3436. Xem trang [giá của Amazon Timestream](https://aws.amazon.com/timestream/pricing/?nc=sn&loc=3) và [Amazon EC2](https://aws.amazon.com/ec2/pricing/) để biết thêm thông tin.

# Điều kiện tiên quyết

Bất kể bạn sử dụng CloudFormation hay Terraform để triển khai tài nguyên, cần đáp ứng một số điều kiện tiên quyết sau:

1.  Hoặc [tạo một EC2 instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/LaunchingAndUsingInstances.html) hoặc sử dụng thiết bị của riêng bạn để triển khai các tài nguyên AWS. Giải pháp trong bài viết này sẽ triển khai thêm một EC2 instance như một bastion host nhằm tuân thủ các security best practices.

2.  Các tệp được sử dụng để triển khai tài nguyên được lưu trữ trong [GitHub repo](https://github.com/awslabs/amazon-timestream-tools) sau đây. Clone kho lưu trữ (repository) này bằng lệnh sau:

    ```bash
    git clone [https://github.com/awslabs/amazon-timestream-tools.git](https://github.com/awslabs/amazon-timestream-tools.git)
    ```

3.  [Cấu hình thông tin xác thực AWS](https://docs.aws.amazon.com/en_us/serverless-application-model/latest/developerguide/serverless-getting-started-set-up-credentials.html) của bạn để sử dụng với [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/using-sam-cli.html) và Terraform. Để biết thêm thông tin, hãy tham khảo [Security best practices trong IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html).

# Tự động hóa giải pháp bằng AWS CloudFormation

Mẫu CloudFormation `template.yml` trong thư mục `amazon-timestream-tools/integrations/cloudformation/ec2-private-influxdb/` định nghĩa một tập hợp các tài nguyên cho phép triển khai một EC2 instance và một Timestream for InfluxDB instance trong private subnet. Chúng ta sẽ triển khai các tài nguyên này bằng SAM CLI.

## Cài đặt SAM CLI

Trên thiết bị của bạn hoặc EC2 instance mà bạn sử dụng để thực thi lệnh, hãy đảm bảo rằng bạn đáp ứng các [yêu cầu tiên quyết](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/prerequisites.html) cho SAM CLI. Sau đó [tải xuống và cài đặt SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html).

Xác minh cài đặt với lệnh:

```bash
sam --version
```

Bạn sẽ nhận được kết quả tương tự như sau:

```text
SAM CLI, version 1.139.0
```

## Triển khai CloudFormation stack

Điều hướng đến thư mục `amazon-timestream-tools/integrations/cloudformation/ec2-private-influxdb/`. Từ thư mục này, chạy lệnh sau để triển khai một stack tên là `Ec2PrivateInfluxDb`:

```bash
sam deploy \
--region <desired AWS Region name> \
-t template.yml \
--parameter-overrides \
ParameterKey=Username,ParameterValue=<username> \
ParameterKey=Password,ParameterValue=<password> \
ParameterKey=Ec2KeyName,ParameterValue=<EC2 key name> \
ParameterKey=ClientIp,ParameterValue=<client IP>
```

Cung cấp các thông tin sau vào các vị trí chứa thông tin:

  * `<desired AWS Region name>`, cung cấp tên vùng AWS mà bạn mong muốn.
  * `<username>`, cung cấp tên người dùng mong muốn, ví dụ, `admin`. Đây sẽ là tên người dùng cho tài khoản quản trị viên ban đầu trong Timestream for InfluxDB instance của bạn.
  * `<password>`, cung cấp mật khẩu mong muốn của bạn.
  * `<EC2 key name>`, cung cấp tên của cặp khóa hiện có mà bạn muốn sử dụng để kết nối với EC2 instance của mình.
  * `<client IP>`, cung cấp địa chỉ IPv4 công khai của thiết bị của bạn, ví dụ, `192.0.2.1`. Một subnet mask là 32 sẽ được sử dụng cho địa chỉ IP này. Việc cung cấp địa chỉ IPv4 công khai của thiết bị sẽ đảm bảo rằng chỉ thiết bị này mới có thể kết nối đến EC2 instance đã triển khai thông qua SSH.

Dưới đây là một ví dụ đầu ra đã được rút gọn:

```text
Deploying with following values
===============================
. . .
Initiating deployment
=====================
Waiting for changeset to be created..
CloudFormation stack changeset
--------------------------------------------------------------------------------------
Operation LogicalResourceId ResourceType Replacement
--------------------------------------------------------------------------------------
+ Add InternetGateway AWS::EC2::InternetGateway N/A
+ Add TimestreamInfluxDBInstance AWS::Timestream::InfluxDBInstance N/A
+ Add VPCGatewayAttachment AWS::EC2::VPCGatewayAttachment N/A
+ Add VPC AWS::EC2::VPC N/A
. . .
--------------------------------------------------------------------------------------
Changeset created successfully. arn:aws:cloudformation:region_name:account_number:changeSet/samcli-deployment_number/id

2025-01-21 12:38:59 - Waiting for stack create/update to complete

CloudFormation events from stack operations (refresh every 5.0 seconds)
. . .
CREATE_COMPLETE AWS::Timestream::InfluxDBInstance TimestreamInfluxDBInstance -
CREATE_COMPLETE AWS::CloudFormation::Stack Racing . . .

Outputs
--------------------------------------------------------------------------
Key TimestreamInfluxDBEndpoint
Description The endpoint of the Timestream for InfluxDB instance.
Value example_endpoint
--------------------------------------------------------------------------
Successfully created/updated stack - Racing in aws_region
```

Kiểm tra mục thông số trong tệp `template.yml` để xem các thông số có sẵn và giá trị mặc định của chúng.

Khi CloudFormation stack hoàn tất việc triển khai, hai đầu ra sẽ được cung cấp:

  * `TimestreamInfluxDBURL`: Địa chỉ URL đầy đủ của Timestream for InfluxDB instance của bạn, bao gồm cả scheme (giao thức) và port (cổng). Bạn có thể sử dụng URL này để ghi dữ liệu vào Timestream for InfluxDB bằng [InfluxDB v2 API](https://docs.influxdata.com/influxdb/v2/reference/api/). Sau đó, bạn sẽ sử dụng endpoint này để ghi dữ liệu vào Timestream for InfluxDB instance.
  * `EC2PublicIP`: Địa chỉ IPv4 công khai của EC2 instance của bạn. Sau này, bạn sẽ sử dụng địa chỉ này để kết nối với EC2 instance của mình thông qua SSH.

Khi giải đua chuyển sang một quốc gia khác, bạn có thể thay đổi giá trị tham số `--region` trong lệnh triển khai SAM CLI sang vùng mới để tạo instance Timestream for InfluxDB mới. Tham khảo hướng dẫn dọn dẹp ở phần sau của bài viết này nếu bạn không còn cần instance cũ.

# Tự động hóa giải pháp bằng Terraform

Terraform là một công cụ quản lý hạ tầng dưới dạng mã (Infrastructure as Code - IaC). Với Terraform, bạn sử dụng ngôn ngữ khai báo [HashiCorp Configuration Language (HCL)](https://developer.hashicorp.com/terraform/language/syntax/configuration) để định nghĩa cấu hình mong muốn cho hạ tầng của mình và để Terraform xử lý phần còn lại. Bạn có thể sử dụng Terraform để quản lý các Timestream for InfluxDB instance bằng tài nguyên [aws\_timestreaminfluxdb\_db\_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/timestreaminfluxdb_db_instance) trong [nhà cung cấp AWS](https://registry.terraform.io/providers/hashicorp/aws/latest).

## Triển khai các tài nguyên Terraform

Để sử dụng Terraform triển khai một EC2 instance và một Timestream for InfluxDB instance trong private subnet, hãy hoàn thành các bước sau:

1.  [Cài đặt Terraform](https://developer.hashicorp.com/terraform/install?product_intent=terraform).

2.  Điều hướng đến `amazon-timestream-tools/integrations/terraform/ec2-private-influxdb/`.

3.  Chạy lệnh sau:

    ```bash
    terraform init
    ```

    Dưới đây là ví dụ về kết quả đầu ra:

    ```text
    Initializing the backend... Initializing provider plugins...
    - Finding hashicorp/aws versions matching "~> 4.16"...
    - Installing hashicorp/aws v4.67.0...
    - Installed hashicorp/aws v4.67.0 (signed by HashiCorp)

    Terraform has created a lock file .terraform.lock.hcl to record the provider selections it made above. Include this file in your version control repository so that Terraform can guarantee to make the same selections by default when you run "terraform init" in the future.

    Terraform has been successfully initialized!

    You may now begin working with Terraform. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform commands should now work.

    If you ever set or change modules or backend configuration for Terraform, rerun this command to reinitialize your working directory. If you forget, other commands will detect it and remind you to do so if necessary.
    ```

4.  Để triển khai tài nguyên, cần thiết lập một số biến. Có một số cách để thiết lập biến:

      * Khi áp dụng thay đổi, nhập giá trị biến khi được yêu cầu:

        ```bash
        terraform apply
        ```

        ```text
        var.ec2_key_name
        Nhập một giá trị:
        ```

        Các biến có giá trị mặc định được định nghĩa trong `variables.tf` sẽ không yêu cầu nhập giá trị.

      * Cung cấp giá trị biến cho Terraform khi áp dụng thay đổi:

        ```bash
        terraform apply -var="ec2_key_name=<example key name>"
        ```

      * Chỉnh sửa `variables.tf`, đặt các giá trị mặc định, ví dụ:

        ```hcl
        variable "ec2_key_name" {
        type = string
        default = "<example key name>" # Added
        }
        ```

5.  Chạy lệnh sau để xem trước các tài nguyên sẽ được triển khai:

    ```bash
    terraform plan
    ```

    Dưới đây là một ví dụ về kết quả đầu ra đã được rút gọn:

    ```text
    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
    + create
    <= read (data resources)

    Terraform will perform the following actions:
    . . .
    # aws_timestreaminfluxdb_db_instance.test_db_instance will be created
    + resource "aws_timestreaminfluxdb_db_instance" "test_db_instance" {
    + allocated_storage = 20
    + arn = (known after apply)
    + availability_zone = (known after apply)
    + bucket = "test-bucket-name"
    + db_instance_type = "db.influx.medium"
    + db_storage_type = "InfluxIOIncludedT1"
    + deployment_type = "SINGLE_AZ"
    + endpoint = (known after apply)
    + id = (known after apply)
    + influx_auth_parameters_secret_arn = (known after apply)
    + name = "Racing"
    + network_type = (known after apply)
    + organization = "organization"
    + password = (sensitive value)
    + port = 8086
    + publicly_accessible = true
    + tags_all = {}
    + username = "admin"
    + vpc_security_group_ids = [
    + (known after apply),
    ]
    + vpc_subnet_ids = [
    + (known after apply),
    ]
    }

    Plan: 12 to add, 0 to change, 0 to destroy.
    ─────────────────────────────────────────────────────────────────
    Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
    ```

6.  Nếu không có lỗi và mọi thứ diễn ra như mong đợi, hãy chạy lệnh sau để triển khai các tài nguyên, nhập "yes" khi được yêu cầu:

    ```bash
    terraform apply
    ```

    Dưới đây là một ví dụ về kết quả đầu ra đã được rút gọn:

    ```text
    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
    + create
    <= read (data resources)

    Terraform will perform the following actions:
    . . .
    # aws_timestreaminfluxdb_db_instance.test_db_instance will be created
    + resource "aws_timestreaminfluxdb_db_instance" "test_db_instance" {
    + allocated_storage = 20
    . . .
    }

    Plan: 12 to add, 0 to change, 0 to destroy.
    Do you want to perform these actions?
    Terraform will perform the actions described above.
    Only 'yes' will be accepted to approve.

    Enter a value: yes
    . . .
    aws_timestreaminfluxdb_db_instance.test_db_instance: Still creating... [13m20s elapsed]
    aws_timestreaminfluxdb_db_instance.test_db_instance: Creation complete after 13m25s [id=db_instance_id]

    Apply complete! Resources: 12 added, 0 changed, 0 destroyed.
    ```

7.  Chờ cho các tài nguyên được triển khai.

Khi Terraform hoàn tất việc triển khai, hai kết quả đầu ra sẽ được cung cấp:

  * `TimestreamInfluxDBURL`: Địa chỉ URL đầy đủ của Timestream for InfluxDB instance của bạn, bao gồm cả scheme (giao thức) và port (cổng). Bạn có thể sử dụng URL này để ghi dữ liệu vào Timestream for InfluxDB bằng [InfluxDB v2 API](https://docs.influxdata.com/influxdb/v2/reference/api/). Sau đó, bạn sẽ sử dụng endpoint này để ghi dữ liệu vào Timestream for InfluxDB instance.
  * `EC2PublicIP`: Địa chỉ IPv4 công khai của EC2 instance của bạn. Sau này, bạn sẽ sử dụng địa chỉ này để kết nối với EC2 instance của mình thông qua SSH.

Trong nhiều ví dụ khác, bao gồm cách thực hiện triển khai Multi-AZ (đa Availability Zone) và bật Amazon S3 logging (ghi log vào Amazon S3), có thể được tìm thấy trong [tài liệu của resource aws\_timestreaminfluxdb\_db\_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/timestreaminfluxdb_db_instance).

## Chỉnh sửa tài nguyên

Bạn có thể chỉnh sửa một tài nguyên đã triển khai bằng cách thay đổi các tệp `main.tf` và `variables.tf`, sau đó lặp lại các bước triển khai. Mặc dù một số thay đổi cập nhật tài nguyên trực tiếp (in-place), nhưng một số thay đổi khác gây ra việc xóa và tạo lại tài nguyên. Một trong những thay đổi đó là thay đổi Region mà tài nguyên của bạn đang chạy. Để triển khai tài nguyên của bạn trên một Region khác, hãy cập nhật biến region trong tệp `variables.tf` thành region mong muốn của bạn:

```hcl
variable "region" {
type = string
default = "us-west-2"
}
```

Thực hiện các bước triển khai để xóa và tạo lại các tài nguyên của bạn trong Region mới.

Với phiên bản 6.0.0 của nhà cung cấp AWS cho Terraform, nhiều tài nguyên đã hỗ trợ tính năng [nhận biết Region](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/guides/enhanced-region-support). Nếu bạn muốn duy trì nhiều tài nguyên trong các Region khác nhau cùng lúc, bạn có thể thêm các định nghĩa tài nguyên mới vào `main.tf` với các giá trị region khác nhau. Ví dụ:

```hcl
resource "aws_timestreaminfluxdb_db_instance" "timestream_influxdb_instance_a" {
# … other configurations
region = "us-east-1"
}

resource "aws_timestreaminfluxdb_db_instance" "timestream_influxdb_instance_b" {
# … other configurations
region = "us-west-2"
}
```

# Gửi dữ liệu đến instance của bạn

Thực hiện các bước sau để mô phỏng dữ liệu chuỗi thời gian từ một giải đua xe thể thao ô tô và nhập nó vào instance đã triển khai của bạn:

1.  Từ thiết bị của bạn, sao chép tập dữ liệu Lap Times từ kho lưu trữ Amazon Timestream Tools sang EC2 instance của bạn. Tập tin line protocol (định dạng giao thức dòng) này chứa thời gian vòng đua từ [Grand Prix Anh 2012](https://en.wikipedia.org/wiki/2012_British_Grand_Prix). Dữ liệu được tổng hợp từ [tập dữ liệu Kaggle của Giải vô địch thế giới Formula 1 (1950–2024)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020) và bao gồm các dấu thời gian được tính toán cho mỗi vòng đua không có trong tập dữ liệu gốc.

    ```bash
    scp -i <path to key> amazon-timestream-tools/sample_apps/data/lap_times.lp ec2-user@<EC2 public IP>:~
    ```

    Thay thế `<path to key>` bằng đường dẫn đến key mà bạn đã chọn để sử dụng với instance và `<EC2 public IP>` bằng địa chỉ IP công khai của EC2 instance của bạn.

2.  Kết nối đến EC2 instance của bạn bằng SSH:

    ```bash
    ssh -i <path to key> ec2-user@<EC2 public IP>
    ```

    Thay thế `<path to key>` bằng đường dẫn đến key mà bạn đã chọn để sử dụng với instance và `<EC2 public IP>` bằng địa chỉ IP công khai của EC2 instance của bạn.

3.  [Tải và cài đặt Influx CLI](https://www.google.com/search?q=https://docs.influxdata.com/influxdb/v2/tools/influx-cli/%3Ft%3DLinux), thay thế `<version>` bằng phiên bản mới nhất của Influx CLI:

    ```bash
    wget [https://dl.influxdata.com/influxdb/releases/influxdb2-client-](https://dl.influxdata.com/influxdb/releases/influxdb2-client-)<version>-linux-arm64.tar.gz
    tar xvzf ./influxdb2-client-<version>-linux-arm64.tar.gz
    sudo cp ./influx /usr/local/bin/
    ```

4.  Để truy cập vào Timestream for InfluxDB instance, bạn sẽ cần một token dành cho vai trò operator (quản trị hệ thống). Hãy tạo token này bằng các lệnh sau:

    ```bash
    influx config create \
    --config-name CONFIG_NAME1 \
    --host-url <Timestream for InfluxDB URL> \
    --org <organization name> \
    --username-password <username>:<password> \
    --active &&
    influx auth create --org <organization name> --operator
    ```

    Để biết thêm thông tin, xem phần [Tạo operator token mới cho InfluxDB instance của bạn](https://docs.aws.amazon.com/timestream/latest/developerguide/timestream-for-influx-getting-started-operator-token.html).

5.  Để nhập dữ liệu vào Timestream for InfluxDB instance của bạn, hãy chạy lệnh sau, thay thế `<Timestream for InfluxDB instance URL>` bằng URL của Timestream for InfluxDB instance của bạn bao gồm cả scheme và port, `<organization name>` bằng tên tổ chức mà bạn đã chỉ định cho instance của mình, `<token>` bằng token từ instance của bạn cho phép ghi vào bucket, và `<Timestream for InfluxDBe bucket name>` bằng tên của bucket Timestream for InfluxDB trong instance của bạn:

    ```bash
    influx write \
    --host <Timestream for InfluxDB instance URL> \
    --org <organization name> \
    --token <token> \
    --bucket <Timestream for InfluxDBe bucket name> \
    --format lp \
    --file ~/lap_times.lp \
    --precision s
    ```

6.  Để xem dữ liệu đã nhập, sử dụng Influx CLI, hãy chạy lệnh sau:

    ```bash
    influx query \
    --host <Timestream for InfluxDB instance URL> \
    --org <organization name> \
    --token <token> \
    'from(bucket: "<Timestream for InfluxDB bucket name>")
    |> range(start: 2012-07-08T11:00:00Z, stop: now())'
    ```

# Dọn dẹp tài nguyên

Trong quá trình triển khai này, bạn đã triển khai một số tài nguyên. Phương pháp dọn dẹp phụ thuộc vào cách các tài nguyên này được tạo ra.

## Dọn dẹp tài nguyên CloudFormation

Để xóa các tài nguyên được triển khai bằng AWS CloudFormation, bao gồm dữ liệu chuỗi thời gian mà instance của bạn có thể chứa, hãy thực hiện các bước sau:

1.  Điều hướng đến `amazon-timestream-tools/integrations/cloudformation/ec2-private-influxdb/`.

2.  Xóa stack của bạn bằng SAM CLI, thay thế `<desired AWS Region name>` bằng vùng mà bạn đã triển khai stack:

    ```bash
    sam delete --region <desired AWS Region name>
    ```

    Dưới đây là kết quả mẫu cho lệnh trước đó:

    ```text
    Are you use you want to delete stack Racing in the region <desired AWS Region name> ? [y/N]: y
    - Deleting Cloudformation stack Racing
    Warning: Cannot resolve s3 bucket information from command options , local config file or cloudformation template. Please use --s3-bucket next time and delete s3 files manually if required.
    Deleted successfully
    ```

## Xóa các tài nguyên Terraform

Để xóa các tài nguyên đã triển khai bằng Terraform, hãy thực hiện các bước sau:

1.  Truy cập vào thư mục `amazon-timestream-tools/integrations/terraform/ec2-private-influxdb/`.

2.  Sử dụng lệnh sau, nhập "yes" khi được yêu cầu:

    ```bash
    terraform destroy
    ```

    Dưới đây là ví dụ về kết quả đầu ra được rút gọn:

    ```text
    aws_timestreaminfluxdb_db_instance.example_db_instance: Refreshing state... [id=db_instance_id]

    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
    - destroy

    Terraform will perform the following actions:
    . . .
    # aws_timestreaminfluxdb_db_instance.test_db_instance will be destroyed
    - resource "aws_timestreaminfluxdb_db_instance" "test_db_instance" {
    - allocated_storage = 20 -> null
    . . .
    }

    Plan: 0 to add, 0 to change, 12 to destroy.
    Do you really want to destroy all resources?
    Terraform will destroy all your managed infrastructure, as shown above.
    There is no undo. Only 'yes' will be accepted to confirm.

    Enter a value: yes
    . . .
    aws_timestreaminfluxdb_db_instance.test_db_instance: Still destroying... [id=abcdefghijkl, 6m41s elapsed]
    aws_timestreaminfluxdb_db_instance.test_db_instance: Destruction complete after 6m49s

    Destroy complete! Resources: 12 destroyed.
    ```

# Tổng kết

Trong bài viết này, chúng tôi đã hướng dẫn cách tự động hóa việc triển khai các Timestream for InfluxDB instance bằng AWS CloudFormation và Terraform, giúp bạn có thể triển khai, xóa hoặc cập nhật cấu hình instance của mình với ít nỗ lực nhất.

Hãy bắt đầu tự động hóa việc triển khai Timestream for InfluxDB cho trường hợp sử dụng của riêng bạn và chia sẻ phản hồi của bạn trong phần bình luận.

# Về tác giả

**Trevor Bonas**

[Trevor](https://www.linkedin.com/in/trevorbonas/) là Nhà phát triển phần mềm cao cấp (Senior Software Developer) tại Improving. Trevor có kinh nghiệm trong việc phát triển cơ sở dữ liệu chuỗi thời gian (time series databases) và trình điều khiển ODBC (ODBC driver development). Trong thời gian rảnh rỗi, Trevor viết truyện hư cấu và thử sức với phát triển trò chơi.

```
````