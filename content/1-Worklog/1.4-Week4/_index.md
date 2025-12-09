---
title: "Week 4 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
  * Successfully deploy Auto Scaling Group (ASG) combined with Application Load Balancer (ALB), mastering the Predictive Scaling strategy for proactive load forecasting.
  * Build a comprehensive monitoring system with CloudWatch, leveraging Logs Insights and Math Expressions for error tracing and in-depth performance analysis.
  * Master NoSQL design with DynamoDB (prioritizing Query/GSI, limiting Scan) and establish a Hybrid DNS model connecting On-premise via Route 53 Resolver.
  * Transition operations from Console to AWS CLI v2, understanding how to interact directly with APIs to manage resources (VPC, S3, IAM) effectively.

### Tasks to Implement This Week:

| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | **TOPIC: HIGH AVAILABILITY WITH ASG & ELB** <br>- **Theory:** <br>  + Understand the mechanism of Amazon EC2 Auto Scaling (ASG) and Application Load Balancer (ALB). <br>  + Analyze Scaling strategies: Manual, Scheduled, Dynamic, and especially Predictive Scaling (using ML to predict load). <br>  + Multi-AZ architecture for RDS Database and Security Groups. <br>- **Practice:** <br>  + Setup infrastructure: Create VPC, launch RDS MySQL (Multi-AZ), and install Node.js environment on EC2. <br>  + Configure Scaling: Create AMI, Launch Template, and set up Target Group for ALB. <br>  + Load Testing: Use Stress Tool to verify the system's auto Scale-out/Scale-in capabilities via Dynamic and Predictive Scaling scenarios. | 29/09/2025 | 29/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | **TOPIC: MONITORING & OPERATIONS WITH AMAZON CLOUDWATCH** <br>- **Theory:** <br>  + Grasp the 4 core components: Metrics, Logs, Alarms, and Dashboards. <br>  + Best Practices for naming and optimizing Log retention settings. <br>- **Practice:** <br>  + Metrics & Math: Customize metric charts, use Math Expressions (Search/Sort) to analyze CPU/Disk data. <br>  + Logs Insights: Configure retention for logs and write queries to filter errors (ERROR/WARN) from the application. <br>  + Alarms & Dashboard: Set up Metric Filters, create Alarms to send alerts via SNS, and aggregate widgets onto a centralized monitoring Dashboard. | 30/09/2025 | 30/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | **TOPIC: BUILDING HYBRID DNS SYSTEM WITH ROUTE 53 RESOLVER** <br>- **Theory:** <br>  + Overview of Hybrid DNS model connecting On-premise and AWS. <br>  + Route 53 Resolver mechanism: Inbound Endpoints (receive queries) and Outbound Endpoints (send queries). <br>  + Understand Forwarding Rules (Resolver Rules). <br>- **Practice:** <br>  + Simulate On-premise: Deploy AWS Managed Microsoft AD and RD Gateway server via CloudFormation. <br>  + Setup Resolver: Create Outbound Endpoint to push queries from AWS to AD and Inbound Endpoint to receive reverse queries. <br>  + Testing: Use `nslookup` and `Resolve-DnsName` to confirm private domain name resolution between the two environments. | 01/10/2025 | 01/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | **TOPIC: NOSQL DATABASE MANAGEMENT WITH AMAZON DYNAMODB** <br>- **Theory:** <br>  + DynamoDB Architecture: Table, Items, Attributes, and Primary Key types (Partition vs Composite). <br>  + Distinguish Scan (scan all) vs Query (query by key) and Global Secondary Index (GSI). <br>  + Consistency models: Eventually Consistent vs Strongly Consistent Reads. <br>- **Practice:** <br>  + Console & CLI: Create Music/Movies tables, perform CRUD (add/delete/edit) items directly on Console and via AWS CloudShell. <br>  + AWS SDK (Boto3): Write Python scripts to interact with DB such as Batch Load data, Query by Index, and Scan with filters. <br>  + Optimization: Practice creating GSI to accelerate queries instead of using Scan. | 02/10/2025 | 02/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | **TOPIC: AUTOMATION & INFRASTRUCTURE MANAGEMENT WITH AWS CLI** <br>- **Theory:** <br>  + Benefits of AWS CLI v2 in automation and direct API interaction. <br>  + Configure Profile, Region, Output format (JSON/Table/Text), and secure Access Keys. <br>- **Practice:** <br>  + Environment Config: Install AWS CLI v2, setup default profile and named profiles. <br>  + Service Management: Use CLI commands to manage S3 (create bucket), SNS (pub/sub), and IAM (create User/Group). <br>  + Build VPC & EC2: Execute command sequences to create VPC, Subnet, IGW, Route Table, and launch EC2 Instances entirely via command line. | 03/10/2025 | 03/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 4:

  * **Scaling Mindset Shift:** Mastered the transition from Reactive (Dynamic Scaling) to Proactive (Predictive Scaling), helping the system automatically prepare resources before peak load times.
  * **Deep Observability:** Went beyond viewing basic metrics; successfully utilized Logs Insights to trace errors (ERROR logs) and Math Expressions to analyze custom data.
  * **NoSQL Optimization:** Deeply understood Access Patterns in DynamoDB, clearly distinguished performance between Scan and Query, and applied Global Secondary Index (GSI) to optimize queries.
  * **Hybrid Connectivity & Automation:** Successfully deployed Hybrid DNS network model with Route 53 Resolver and mastered infrastructure management via AWS CLI instead of relying solely on the Console.

### Challenges – Solutions:

  * **Challenge:** DynamoDB Performance – Difficulty distinguishing when to use Scan vs. Query, concerned about consuming Read Capacity Units (RCU) with large data.
      * **Solution:** Applied "Query First" strategy. Used Global Secondary Index (GSI) to create different data views, enabling the use of Query commands instead of scanning the entire table.
  * **Challenge:** Predictive Scaling not working immediately – When first configured, ASG could not predict load due to lack of historical data (needs at least 2 days).
      * **Solution:** Executed scripts to simulate historical data and injected Custom Metrics into CloudWatch to "train" the AWS Machine Learning model to understand system patterns.
  * **Challenge:** AWS CLI Operations – Output returned as JSON was too long and hard to read; difficult to extract the ID of the newly created resource for the next command.
      * **Solution:** Used the `--query` parameter to filter exactly the necessary data fields and `--output text/table` to display results visually, making them easy to reuse in scripts.

### Lessons Learned:

  * In a Cloud environment, **predictability** is the key to balancing Performance and Cost. Predictive Scaling helps us prepare in advance rather than just reacting to incidents.
  * Collecting Logs and Metrics is only valuable when it triggers a specific action (Alarms, Auto Scaling) or helps answer "Why?" quickly (Logs Insights). Otherwise, it is just a waste of storage costs.
  * Unlike SQL, with DynamoDB we must define **Access Patterns** before designing the table. Choosing the wrong Primary Key or Index from the start will lead to significant performance and cost consequences later.
