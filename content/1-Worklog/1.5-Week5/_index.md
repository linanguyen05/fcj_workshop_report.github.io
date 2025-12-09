---
title: "Week 5 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
  * Eliminate Bastion Hosts and traditional ports (22/3389) by adopting "Zero Trust" server management with AWS Systems Manager (Session Manager).
  * Implement private connectivity for internal resources using VPC Endpoints (PrivateLink) and secure Audit Logging.
  * Automate infrastructure provisioning using CloudFormation (Infrastructure as Code), handling advanced scenarios like Custom Resources and Drift Detection.
  * Secure web applications against common vulnerabilities (OWASP) using AWS WAF.
  * Implement data encryption and key management strategies with AWS KMS and auditing with CloudTrail.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | **TOPIC: SERVER MANAGEMENT WITHOUT BASTION HOST (SSM PART 1)** <br> - **Theory:** <br>  + **Session Manager:** Learn the mechanism to replace traditional SSH/RDP, completely removing Bastion Hosts. <br>  + **Security Architecture:** Analyze IAM Role model combined with SSM Agent and TLS 1.2 protocol. <br>  + **Benefits:** Reduce attack surface by not opening port 22 (Linux) or 3389 (Windows) to the Internet. <br> - **Practice:** <br>  + **Network Setup:** Create VPC & Subnets (Public/Private) preparing for the lab environment. <br>  + **Security Group (Zero Trust):** Configure SG to close all Inbound traffic, allowing only Outbound HTTPS. <br>  + **Basic Connection:** Launch EC2 (Linux & Windows), attach `AmazonSSMManagedInstanceCore` IAM Role, and connect directly via browser. | 06/10/2025 | 06/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | **TOPIC: PRIVATE CONNECTIVITY & AUDIT LOGGING (SSM PART 2)** <br> - **Theory:** <br>  + **VPC Endpoints (PrivateLink):** Understand how Private Instances communicate with AWS Services internally without an Internet Gateway. <br>  + **Port Forwarding:** Tunneling technique for secure RDP/SSH access. <br> - **Practice:** <br>  + **Endpoint Configuration:** Deploy 3 Interface Endpoints (`ssm`, `ssmmessages`, `ec2messages`) for Private Subnet. <br>  + **Log Management:** Create S3 Gateway Endpoint and configure Session Manager to push command history to S3 bucket (encrypted). <br>  + **Advanced Connection:** Install AWS CLI and Plugin on local machine, perform Port Forwarding to RDP into Private Windows Instance (Port 3389 -\> Localhost 9999). | 07/10/2025 | 07/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | **TOPIC: INFRASTRUCTURE AS CODE (CLOUDFORMATION)** <br> - **Theory:** <br>  + **Template Structure:** Master components like Parameters, Resources, Outputs, and intrinsic functions (`!Ref`, `!Sub`, `!GetAtt`). <br>  + **Drift Concept:** Understand the discrepancy between actual configuration and code configuration. <br> - **Practice:** <br>  + **Environment:** Setup AWS Cloud9 IDE for coding. <br>  + **Write Template:** Build YAML file to automate Security Group, IAM Role, and EC2 Instance creation. <br>  + **Custom Resources:** Use Lambda Function to create SSH Key Pair and store in Parameter Store (handling tasks not natively supported by CFN). <br>  + **StackSets & Drift:** Deploy infrastructure across multiple Regions and practice configuration drift detection. | 08/10/2025 | 08/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | **TOPIC: PROTECTING WEB APPLICATIONS WITH AWS WAF** <br> - **Theory:** <br>  + **Web ACL & Rules:** Distinguish AWS Managed Rules (pre-configured) and Custom Rules (user-defined). <br>  + **Logic:** Understand Block, Allow, Count actions and JSON structure for complex rules. <br> - **Practice:** <br>  + **Deployment:** Deploy OWASP Juice Shop sample app via CloudFormation and create Web ACL protection. <br>  + **Apply Rules:** Activate Managed Rules (Core Rule Set, SQL Database) to block SQL Injection and XSS. <br>  + **Custom Rules:** Write custom rules using JSON (AND/OR logic) to block specific Headers or Query Strings. <br>  + **Logging:** Configure Kinesis Data Firehose to push WAF logs to S3, setting Redacted Fields to hide sensitive info (Cookie/Auth Token). | 09/10/2025 | 09/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | **TOPIC: ENCRYPTION & KEY MANAGEMENT (KMS & CLOUDTRAIL)** <br> - **Theory:** <br>  + **Key Management:** Distinguish Symmetric and Asymmetric Keys. <br>  + **SSE-KMS:** Server-side Encryption mechanism integrated with S3. <br> - **Practice:** <br>  + **Key Governance:** Create Customer Managed Key (CMK), set Alias, and enable automatic Key Rotation. <br>  + **S3 Security:** Create Bucket enforcing KMS encryption, test access permissions (User without Key permission is blocked even with S3 permission). <br>  + **Audit & Share:** Use CloudTrail and Athena to query access logs. Practice secure file sharing using time-limited Presigned URLs. <br>  + **Cleanup:** Execute secure resource deletion (Schedule Key Deletion, Delete Stack/Buckets) to optimize costs. | 10/10/2025 | 10/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 5:

  * **Zero Trust Server Management:** Completely removed dependency on Bastion Hosts and opening ports 22/3389. Successfully operated Session Manager combined with VPC Endpoints to manage Private Instances without an Internet Gateway.
  * **Infrastructure Automation (IaC):** Shifted mindset from manual operations to Infrastructure as Code with CloudFormation. Handled advanced challenges like Custom Resources (using Lambda for Keys) and Resource Drift Control.
  * **Defense in Depth:** Implemented multi-layered security: Application Firewall WAF (Layer 7) preventing OWASP vulnerabilities, and Data Encryption with KMS (Data Layer), ensuring safety from transmission to storage.

### Challenges – Solutions:

  * **Challenge:** SSM Agent on Private Instance was Offline.
      * **Solution:** Reviewed network infrastructure. Added all 3 required endpoints (`ssm`, `ssmmessages`, `ec2messages`) to the Private Subnet and ensured the Endpoint's Security Group allowed Port 443 from the VPC CIDR.
  * **Challenge:** S3 file configured as "Make Public" but access resulted in Access Denied/Signature error.
      * **Solution:** The file was encrypted with a KMS Key, and anonymous users do not have decryption permissions. Switched to using **Presigned URL** for secure, time-limited file sharing instead of opening Public ACL.
  * **Challenge:** WAF Rule blocked valid users (False Positive) during initial deployment.
      * **Solution:** Changed deployment process. Always set Action to **"Count"** first to monitor Metrics on CloudWatch; only switch to **"Block"** after confirming no impact on real users.

### Lessons Learned:
  * In a Cloud environment, security is not just about blocking IPs. **Identity management (IAM Role)** granting permissions to servers and services (Service-to-Service) is core, replacing the traditional open-port mindset.
  * Apply **Defense in Depth**: Network (VPC/SG) -\> Application (WAF) -\> Data (KMS). Even if an S3 file path is exposed (Public), attackers cannot read the content without the Decryption Key.
