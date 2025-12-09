---
title: "Week 3 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

  * Master IAM Role configuration for EC2, understanding the Security Token Service (STS) mechanism for granting temporary permissions instead of embedding Access Keys.
  * Fully deploy a secure S3 Static Website (BPA) accelerated via CloudFront (using OAI).
  * Practice key S3 management features, including S3 Versioning and Cross-Region Replication (CRR).
  * Build a 3-tier network infrastructure (Web - App - DB) on AWS with VPC, Security Groups (separating EC2/RDS), and DB Subnet Groups (Multi-AZ).
  * Deploy a Node.js application connecting to Amazon RDS (MySQL).
  * Understand restore operations (Snapshot) and clearly distinguish Multi-AZ from Read Replicas.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | - **Theory Research:**<br>  + Two permission methods: Access Key (embedded key, high risk) and IAM Role (temporary info, secure, recommended).<br>  + Understand IAM Role mechanism on EC2 (EC2 Instance Profile) and the role of Security Token Service (STS).<br>- **Practice:**<br>  + Setup environment (EC2 t2.micro, S3 Bucket).<br>  + *Access Key:* Create IAM User, grant Programmatic access, embed Access Key in Python code (boto3) to upload file to S3.<br>  + *Security (IAM Role):* Successfully configure IAM Role (Instance Profile) for EC2; AWS CLI automatically detects permissions via metadata without credentials file.<br>  + Cleanup resources (EC2, S3, IAM User/Role). | 22/09/2025 | 22/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | - **Theory Research:**<br>  + Overview of AWS Cloud9: An integrated browser-based IDE, providing code editor, debugger, and integrated terminal.<br>  + AWS CLI is pre-installed and configured on Cloud9.<br>- **Practice:**<br>  + Setup Cloud9 environment (t2.micro). **Note:** Cloud9 automatically manages the backend EC2 and pre-installs AWS CLI.<br>  + Basic operations with integrated terminal and code editor (open, edit, save files).<br>  + Verify AWS CLI success: `aws ec2 describe-instances`.<br>  + Cleanup: Delete Cloud9 environment. | 23/09/2025 | 23/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | - **Theory Research:**<br>  + Amazon S3: Object storage service (11 9s durability). Distinguish Bucket (globally unique name) and Object.<br>  + S3 Features: Static Website Hosting, S3 Versioning (anti-deletion/overwrite, creates "delete marker"), Cross-Region Replication (CRR) (disaster recovery, requires Versioning).<br>  + Security & Performance: Block Public Access (BPA) (should always be on). Use CloudFront with OAC (Origin Access Control) for security and acceleration (distribute via Edge Locations). | 24/09/2025 | 24/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | - **Practice:**<br>  + *Phase 1 (Public S3):* Deploy S3 Static Website. Temporarily disable Block Public Access (BPA) and configure ACLs (Make public using ACL) to publicize website (note: not recommended).<br>  + *Phase 2 (Private S3 + CloudFront):* Reconfigure security: Enable BPA (=\> private bucket). Integrate CloudFront with OAI (Origin Access Identity), allowing CloudFront to access S3 while blocking public access.<br>  + **Result:** Page load speed significantly improved when accessed via CloudFront URL.<br>  + *Phase 3 (Features):* Activate S3 Versioning to test recovery capabilities. Configure Cross-Region Replication (CRR) to another region.<br>  + Cleanup resources (CloudFront, S3 Buckets). | 25/09/2025 | 25/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | - **Theory Research:**<br>  + Amazon RDS: Managed Relational DB service (for OLTP), automated patching, backup.<br>  + HA/DR: Distinguish Multi-AZ (HA, synchronous replication, auto failover) and Read Replicas (Read scaling, asynchronous replication).<br>  + Network: Role of DB Subnet Group (needs at least 2 AZs for Multi-AZ) and Security Group (open port 3306 only from EC2 SG).<br>- **Practice:**<br>  + **Lesson:** Build network infrastructure and deploy 3-tier app (Web - App - DB).<br>  + *Network Prep (Foundation):* Complete VPC infrastructure setup. **Key Note:** Configuring 2 separate Security Groups (EC2, RDS) and DB Subnet Group (using 2 AZs) is a prerequisite for RDS secure operation and Multi-AZ support.<br>  + *Deployment:* Launch EC2 (Web server) and RDS (MySQL). Install Node.js app on EC2 and successfully connect to RDS endpoint.<br>  + *DB Operation:* Execute SQL script to create schema. **Test snapshot restore, note:** RDS creates a *new* instance with a *new* endpoint (requires app config update).<br>  + Cleanup all resources (RDS, EC2, VPC). | 26/09/2025 | 26/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 3:

  * Clearly distinguished and correctly applied access permission methods.
  * Successfully deployed a secure and high-performance Static Website.
  * Mastered the process of deploying network infrastructure and 3-tier applications: Understood the logic and sequence of network setup. Successfully configured core components: VPC, Security Group (separating EC2 and RDS SGs), and DB Subnet Group (preparing for Multi-AZ).
  * Basic operation of Amazon RDS. When restoring from a DB Snapshot, RDS creates a new DB instance with a new endpoint, requiring connection string updates in the application.

### Challenges – Solutions:

  * **Challenge:** Configured Cross-Region Replication (CRR) but new files uploaded to source bucket did not auto-copy to destination bucket.
      * **Solution:** Re-checked S3 IAM Role. Required granting `s3:GetReplicationConfiguration` and `s3:ListBucket` for the source bucket, and `s3:ReplicateObject` for the destination bucket.
  * **Challenge:** Application on EC2 could not connect to RDS Database (timeout error).
      * **Solution:** Checked RDS Security Group. Port 3306 (MySQL) was open but Source was set to EC2's public IP; changed Source to EC2's **Security Group ID** to ensure safe internal connection within VPC.

### Lessons Learned:

  * **Security is priority:**
      * Do not hardcode credentials (Access Keys). Use IAM Roles for AWS resources (like EC2) to grant temporary permissions.
      * Always enable Block Public Access (BPA) for S3. Only allow S3 access via trusted services (like CloudFront OAI/OAC).
      * Do not open admin ports (SSH) or DB ports (3306) to 0.0.0.0/0. Must restrict source IPs (for SSH) or restrict via Security Group (for DB).
  * **Endpoints:** When working with services (S3 Static Website, CloudFront, RDS), the endpoint (URL) is the key to access. Any change regarding the endpoint (such as RDS restore or switching to CloudFront) must be updated on the application side.
  * **Managed features** such as S3 Versioning (data protection), Multi-AZ (increased HA), and Cloud9 cost-saving (cost optimization) help optimize operations.
