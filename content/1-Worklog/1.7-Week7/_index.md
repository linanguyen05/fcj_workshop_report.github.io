---
title: "Week 7 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

  * **Mid-term Exam Review:** Apply comprehensive knowledge of **Secure & Resilient Architectures** (IAM, VPC, Multi-AZ) and **Serverless** to successfully complete the phase 1 capability assessment.
  * **Intro to DevOps & CI/CD on AWS:** Begin the transition from manual deployment to automation. Research the **AWS Developer Tools** suite (CodeCommit, CodeBuild, CodePipeline) to build continuous integration and deployment pipelines.

### Tasks to Implement This Week:

| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | **TOPIC: SERVERLESS ARCHITECTURE ON AWS** <br>- **Theory & Architecture:** <br>  + Understand Serverless model, "Pay-as-you-go" mechanism, and the role of AWS Lambda combined with Amazon S3. <br>  + Analyze Event-driven processing flow: Upload image (S3) $\rightarrow$ Trigger $\rightarrow$ Resize $\rightarrow$ Storage. <br>- **Practice:** <br>  + Image Processing: Write Lambda Function (Node.js), configure environment variables, and set up S3 Trigger (All object create events). <br>  + Data Management: Create DynamoDB table (On-demand) and write Lambda (Python) to store book metadata. <br>  + Security: Configure IAM Policy adhering to Least Privilege principles. | 20/10/2025 | 20/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | **TOPIC: BUILDING SERVERLESS APPLICATION (FULL STACK)** <br>- **Foundational Theory:** <br>  + Amazon API Gateway: The "gateway" role managing traffic, authentication, and API types (RESTful). <br>  + S3 Static Web Hosting: Mechanism for storing and distributing web Frontends without servers. <br>- **Practice:** <br>  + Frontend Deployment: Build ReactJS source code, upload to S3 bucket, and configure public access permissions. <br>  + Backend Development: Develop Lambda function chain handling CRUD operations (Create, Read, Delete). <br>  + System Integration: Setup API Gateway, handle CORS issues, and connect Frontend with Backend via API Endpoint. | 21/10/2025 | 21/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | **TOPIC: ORDER PROCESSING SYSTEM (DECOUPLING ARCHITECTURE)** <br>- **System Architecture:** <br>  + Asynchronous Model: Decouple system components to increase scalability. <br>  + Messaging Services: Use Amazon SQS as a load buffer and Amazon SNS to send notifications. <br>- **Practice:** <br>  + Infrastructure as Code: Use AWS SAM to define and deploy the entire stack (API, Lambda, DB, Queue). <br>  + Logic Processing: Configure Lambda to push messages to Queue and Worker to process orders from Queue into DynamoDB. <br>  + Testing & Verify: Execute End-to-End flow from ordering, checking SQS flight-mode to receiving SNS email. | 22/10/2025 | 22/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | **TOPIC: REVIEWING SECURE ARCHITECTURES** <br>- **Research Content:** <br>  + Access Management: Deep dive into IAM Roles, Policies, MFA, and Service Control Policies (SCP). <br>  + Infrastructure Protection: Distinguish Security Groups (Stateful) and NACLs (Stateless). <br>  + Advanced Security Services: AWS WAF, AWS Shield, GuardDuty, and Secrets Manager. <br>- **Practice:** <br>  + Security Audit: Review Security Groups and IAM Roles established in this week's labs. <br>  + Encryption: Research encryption at rest (KMS) and in transit (TLS/ACM). | 23/10/2025 | 23/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | **TOPIC: REVIEWING RESILIENT ARCHITECTURES** <br>- **Research Content:** <br>  + High Availability: Multi-AZ and Multi-Region design. <br>  + Disaster Recovery: Strategies from Backup & Restore to Multi-site Active/Active. <br>  + Scalability: Review EC2 Auto Scaling, DynamoDB Scaling, and Route 53 Routing Policies. <br>- **Practice:** <br>  + Cleanup: Delete SAM Stack, Empty S3 Buckets, and delete DynamoDB Tables to avoid incurring costs. | 24/10/2025 | 24/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 7:

  * **Proficient Operation of Event-Driven Model:**
      * Successfully built an automated flow: S3 Event Trigger activates Lambda Function to process images and store metadata, completely eliminating manual intervention.
  * **Comprehensive Full-stack Serverless Deployment:**
      * Completed Book Store application with Frontend (S3 Static Hosting) communicating securely with Backend via Amazon API Gateway.
      * Designed DynamoDB database in On-demand mode suitable for unstable workloads.
  * **Realization of Decoupling Architecture:**
      * Successfully applied Amazon SQS (Queue) and Amazon SNS (Topic) to process orders asynchronously, helping the system withstand high loads and ensuring user experience is not interrupted.
  * **Mastery of Infrastructure as Code (IaC) with AWS SAM:**
      * Instead of error-prone manual operations, learned how to define, build, and deploy complex stacks (API, DB, Lambda, Queue) via `template.yaml` source code.

### Challenges – Solutions:

  * **Challenge: Cross-Origin (CORS) Connection Error between Frontend and Backend**
      * Frontend on S3 was blocked by the browser when calling API Gateway.
      * **Solution:** Configured Enable CORS on API Gateway for all methods (GET, POST, DELETE). Most importantly, **Redeploy API** immediately after configuration changes for them to take effect.
  * **Challenge: Lambda Function "Access Denied" Error when Accessing Resources**
      * Function could not write files to destination S3 bucket or scan DynamoDB table.
      * **Solution:** Checked CloudWatch Logs to identify missing permissions. Updated Lambda IAM Role following specific permission principles (Inline Policy) instead of using overly broad FullAccess.
  * **Challenge: Duplicate Message Processing in Amazon SQS**
      * Order was saved to Database but message remained in Queue (Flight mode) leading to potential reprocessing.
      * **Solution:** Reviewed logic code in Lambda Worker (`handle_order`), ensuring `sqs.delete_message` command is executed immediately after successful Database write task (within `try...except` block).

### Lessons Learned:

  * **Power of Asynchronous Architecture:**
      * Placing SQS between Frontend and Backend is the key for large-scale systems, acting as a "shock absorber" (buffer) when traffic spikes without crashing the Database.
  * **Least Privilege Principle is Vital:**
      * In Lab environments, broad permissions might be used, but in reality (Production), permissions must be restricted to specific Resource ARNs to ensure system security.
  * **"Design for Failure" Mindset:**
      * Systems should not be designed to "never fail," but must have the ability to self-recover. Using Auto Scaling, Multi-AZ, and Route 53 Failover is mandatory to ensure resilience.

