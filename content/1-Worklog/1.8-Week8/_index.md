---
title: "Week 8 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:
* **Mastering Serverless CI/CD workflows:** Successfully designed and deployed a fully automated (End-to-End) pipeline for Full-stack applications, integrating Gitlab with the AWS CodeSuite ecosystem (CodePipeline, CodeBuild) and CloudFormation.
* **Constructing modern Data Lakes & Optimizing Big Data:** Executed the complete data processing workflow from Ingestion, data cleaning (DataBrew), ETL conversion to Parquet format (Glue), to query analysis (Athena) and visualization (QuickSight).
* **Reinforcing architectural mindset & Completing assessment:** Systematized knowledge of the AWS Well-Architected Framework (focusing on Performance & Cost Optimization) and completed the Mid-term Exam to validate real-world system design capabilities.

### Tasks to be carried out this week:
| Day | Task | Start Date | End Date | Resources |
| :--- | :--- | :--- | :--- | :--- |
| Mon | **TOPIC: SERVERLESS CI/CD IMPLEMENTATION WITH AWS CODEPIPELINE** <br> - **Theory:** <br>  + [cite_start]Understand Serverless CI/CD architecture: Automating the Build, Package, and Deploy process for Full-stack applications[cite: 54, 55]. <br>  + [cite_start]AWS SAM Pipelines mechanism: Bootstrapping multi-platform pipelines (Gitlab, Jenkins, CodePipeline)[cite: 56, 58]. <br>  + [cite_start]AWS CodeSuite services: CodePipeline (Orchestration), CodeBuild (Compiling), CloudFormation (IaC)[cite: 60, 61, 62]. <br> - **Practice:** <br>  + [cite_start]**Environment Setup:** Configure IAM Roles adhering to the Least Privilege principle[cite: 66, 86]. <br>  + [cite_start]**Backend Pipeline:** Create Gitlab Repo, configure `buildspec.yml`, and connect the pipeline to deploy the SAM Template[cite: 67, 69, 70]. <br>  + [cite_start]**Frontend Pipeline:** Update API Endpoint, configure ReactJS/VueJS build, and auto-deploy artifacts to S3 bucket[cite: 74, 75, 77]. <br>  + [cite_start]**Integration Test:** Perform End-to-End testing (Register -\> Login -\> Create Book) integrated with Cognito[cite: 79, 81]. | 27/10/2025 | 27/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | **TOPIC: BUILDING DATA LAKE ON AWS** <br> - **Theory:** <br>  + [cite_start]Data Lake on S3 Concept: Centralized storage for Raw and Processed data[cite: 3, 100]. <br>  + [cite_start]AWS Glue Ecosystem: Glue Crawler (Schema discovery), Data Catalog (Metadata management), and ETL Jobs[cite: 6, 7, 8]. <br>  + [cite_start]Performance: Comparing Row-based (CSV) vs. Columnar (Parquet) formats for Big Data queries[cite: 48, 49, 125]. <br> - **Practice:** <br>  + [cite_start]**Ingestion & Prep:** Initialize Cloud9, check encoding, and upload the Airbnb dataset to S3[cite: 101, 104, 105]. <br>  + [cite_start]**Data Cleaning:** Use Glue DataBrew (No-code) for data profiling, cleaning, and schema normalization[cite: 110, 114, 119]. <br>  + [cite_start]**ETL Transformation:** Write Glue Jobs (Spark/Python) to convert CSV to Parquet and implement Partitioning to optimize costs[cite: 30, 38, 50]. <br>  + [cite_start]**Analytics & BI:** Run interactive SQL queries with Amazon Athena and visualize data on QuickSight (Pie Chart, Scatter Plot)[cite: 39, 42, 156]. | 28/10/2025 | 28/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | **TOPIC: DESIGNING HIGH-PERFORMING ARCHITECTURES** <br> - **Knowledge Review:** <br>  + **Compute Scaling:** EC2 Auto Scaling mechanisms, Lambda concurrency, and Fargate scaling. <br>  + **Storage Performance:** Optimizing IOPS for EBS, throughput for EFS, and S3 storage classes. <br>  + **Network Optimization:** Reducing latency with CloudFront (CDN) and AWS Global Accelerator. <br>  + **Database Caching:** Caching strategies with ElastiCache and network optimization. <br> - **Preparation:** <br>  + Review critical CloudWatch Metrics for triggering effective Scaling policies. | 29/10/2025 | 29/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | **TOPIC: DESIGNING COST-OPTIMIZED ARCHITECTURES** <br> - **Knowledge Review:** <br>  + **Cost Management:** Analyzing costs with Cost Explorer and setting budget alerts with AWS Budgets. <br>  + **Pricing Models:** Comparing and selecting between On-Demand, Savings Plans, and Spot Instances. <br>  + **Storage Optimization:** Configuring S3 Lifecycle Policies for automatic storage tiering. <br>  + **Network Costs:** Optimizing data transfer costs via NAT Gateway and VPC Peering. <br> - **Preparation:** <br>  + Review scenarios for cost allocation tags. | 30/10/2025 | 30/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | **TOPIC: MID-TERM EXAM** <br> - **Exam Content:** <br>  + **Secure Architectures:** IAM, MFA, KMS Encryption, Security Groups, NACLs, WAF, Shield. <br>  + **Resilient Architectures:** Multi-AZ, Multi-Region, DR Strategies, Route 53. <br>  + **High-Performing & Cost-Optimized:** Concepts reviewed earlier in the week. <br>  + **Well-Architected Framework:** Applying the 6 pillars to real-world system design. <br> - **Activities:** <br>  + Complete the multiple-choice exam and practical Lab. <br>  + Summarize results and identify knowledge gaps for improvement. | 31/10/2025 | 31/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |


### Week 8 Achievements:
* **Successfully deployed a fully automated Serverless CI/CD system:** Integrated Gitlab with AWS CodePipeline to build Backend (SAM/CloudFormation) and deploy Frontend (S3 Static Website) via `buildspec.yml` configuration.
* **Built an industry-standard Data Lake process on S3:** Proficiently applied AWS Glue Crawler for automatic schema discovery, used Glue DataBrew for data cleaning, and executed Glue Jobs for ETL.
* **Optimized Big Data query performance:** Verified and compared the superior efficiency of Parquet format (Columnar) versus CSV (Row-based) when querying with Amazon Athena (faster speed, ~10x lower scanning cost).
* **Systematized AWS architectural thinking (Well-Architected):** Mastered Auto Scaling strategies (distinguishing Dynamic vs. Predictive Scaling) and storage cost optimization models (S3 Lifecycle Policies, Savings Plans) in preparation for the mid-term exam.

### Challenges – Solutions:
* API connection error (Network Error) between Frontend and Backend after pipeline deployment
  * *Solution:* Checked Frontend configuration. Retrieved the `ApiUrl` from the CloudFormation Stack Output (Backend), updated it in the `src/config.js` file, and committed the code to trigger a pipeline rebuild.

* AWS Glue Crawler identified wrong Data Types or character encoding errors
  * *Solution:* Used AWS Glue DataBrew to run a Profile job for data quality checks first. Used the `enca` tool in the Cloud9 environment to standardize encoding to UTF-8 for CSV files before pipeline processing.

* CodeBuild encountered "Access Denied" when attempting to push artifacts to S3 Bucket
  * *Solution:* Reviewed the IAM Role assigned to the CodeBuild Project. Added `s3:PutObject` permission for the specific target bucket ARN (adhering to the Least Privilege principle) instead of granting broad Admin rights.

### Lessons Learned:
* Data Format Matters
  * In Big Data processing on the Cloud, converting data to a columnar format (like Parquet) is not just a technical step but a core cost optimization strategy ("scanning less means paying less").

* Automation is the key to stability (Automation for Stability)
  * CI/CD Pipelines not only speed up deployment but also eliminate human errors. Investing time to write a standard `buildspec.yml` from the beginning saves significant operational debugging time later.

* "Design for Failure" Mindset
  * Every infrastructure component can fail. Therefore, system architecture must always be Decoupled, deployed across multiple zones (Multi-AZ), and possess self-healing mechanisms (Auto Scaling) rather than relying on a single node.