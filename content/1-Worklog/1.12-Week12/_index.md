---
title: "Week 12 Worklog"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:
* Understand and execute architectural migration from traditional models (RDS/VPC) to pure Serverless (No-VPC) to optimize operational costs.
* Successfully deploy an AI data processing flow (RAG Pipeline) combining Vector Database (Pinecone) and Key-Value Store (DynamoDB) to replace SQL.
* Master Code Refactoring techniques for AWS Lambda: Transition from `psycopg2` to `boto3`, managing connections and handling Cold Starts.
* Establish a "Monitoring as Code" mindset: Automate error and performance alerting setup for the system using CloudWatch and Scripting.
  
### Tasks to be carried out this week:
| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| 2 | **SUBJECT: DESIGNING RAG ARCHITECTURE & VECTOR DATABASE** <br> - **AI/ML Solution Research:** <br>  + Analyze the **RAG (Retrieval-Augmented Generation)** model to optimize AI responses using custom data. <br>  + Understand **Vector Database (Pinecone)** concepts and Embedding models (`cohere.embed-multilingual-v3.0`). <br> - **Practice:** <br>  + **Pinecone Initialization:** Configure Index (Name: `metaphysical-index`, Dimension: `1024`, Metric: `Cosine`) compatible with Cohere. <br>  + **Environment Setup:** Install necessary libraries (`pinecone-client`, `langchain`) for local development. | 24/11/2025 | 24/11/2025 | |
| 3 | **SUBJECT: DATA MIGRATION - FROM SQL TO NOSQL & VECTOR** <br> - **ETL Strategy (Extract-Transform-Load):** <br>  + Design **Amazon DynamoDB** table (On-demand capacity) to replace RDS PostgreSQL for high-speed key-value access. <br>  + Data Flow Planning: Store Metadata in DynamoDB and Vector Embeddings in Pinecone. <br> - **Practice:** <br>  + Create DynamoDB table `MetaphysicalKnowledgeBase`. <br>  + **ETL Scripting:** Migrate data from `dataset_v3.jsonl`/RDS -\> Generate Embeddings -\> Upsert to Pinecone and DynamoDB. <br>  + **Troubleshooting:** Debug and resolve ID Mismatches between Pinecone vectors and DynamoDB items. | 25/11/2025 | 25/11/2025 | |
| 4 | **SUBJECT: LAMBDA REFACTORING - PYTHON BACKEND OPTIMIZATION** <br> - **Serverless Coding Techniques:** <br>  + Shift mindset from stateful (SQL connection pools) to stateless (HTTP API calls via Boto3). <br>  + Optimize **Cold Starts** by managing Global Variables and Init Context. <br> - **Practice:** <br>  + **Code Refactoring:** Rewrite "Tarot/Horoscope" Lambda logic. Remove `psycopg2` dependencies (RDS) and implement `boto3` (DynamoDB). <br>  + **Bedrock Integration:** Implement RAG flow (Query Pinecone -\> Fetch Context -\> Invoke Claude 3 Sonnet). <br>  + **Debugging:** Resolve runtime errors related to library layers and IAM permissions. | 26/11/2025 | 26/11/2025 | |
| 5 | **SUBJECT: INFRASTRUCTURE MODERNIZATION - TRANSITIONING TO NO-VPC** <br> - **Cost & Performance Optimization:** <br>  + Analyze benefits of **Lambda No-VPC** architecture: Eliminate ENI creation latency and remove expensive NAT Gateway costs. <br>  + Assess security implications when moving to public endpoints with IAM Auth. <br> - **Practice:** <br>  + **Network Config:** Detach Lambda Functions from VPC subnets and security groups. <br>  + **Resource Cleanup:** Terminate RDS Instances, delete VPC Endpoints, and remove unused NAT Gateways. <br>  + **System Testing:** Verify all features post-migration to ensure reduced latency and stable connectivity. | 27/11/2025 | 27/11/2025 | |
| 6 | **SUBJECT: MONITORING STRATEGY - AUTOMATED OBSERVABILITY** <br> - **Operational Excellence:** <br>  + Define "Golden Signals" for Serverless monitoring: Errors, Throttles, Duration, and Concurrent Executions. <br>  + Adopt "Monitoring as Code" approach (Scripting vs. ClickOps). <br> - **Practice:** <br>  + **CloudWatch Automation:** Use **AWS CloudShell** to write Bash/CLI scripts for automatically creating Alarms for all Lambda functions. <br>  + **Alarm Configuration:** Set thresholds (e.g., Error Rate \> 1%, Duration \> 25s) to prevent timeouts. <br>  + **Acceptance Testing:** Validate the notification flow via SNS by triggering intentional errors. | 28/11/2025 | 28/11/2025 | |


### Week 12 Achievements:
* **Architecture Modernization:** Successfully transitioned the system to a **pure Serverless (No-VPC)** architecture. This eliminated fixed costs associated with NAT Gateways and RDS, effectively bringing infrastructure costs to nearly $0 when idle.
* **RAG Pipeline Deployment:** Built a hybrid AI data processing flow using **Pinecone** for Semantic Search and **DynamoDB** for high-speed Metadata retrieval, completely replacing complex SQL queries.
* **Operational Automation:** Moved away from manual "ClickOps" by developing **AWS CloudShell** scripts to automatically configure CloudWatch Alarms for all Lambda Functions, ensuring immediate system observability.
* **Performance Optimization:** Reduced application latency by detaching Lambda from the VPC (eliminating ENI initialization time) and refactoring database logic from `psycopg2` to `boto3`.

### Challenges – Solutions:
* Data Consistency issues between Vector DB and NoSQL DB (ID mismatch), causing the AI to retrieve incorrect contexts.
  * Solution: Rewrote the ETL process, implemented ID normalization during the Preprocessing stage before ingestion, and performed step-by-step debugging to ensure alignment.

* Lambda experienced Timeouts and high Cold Starts when initializing connections to Bedrock and Pinecone.
  * Solution: Optimized Python code by moving Client initialization (Pinecone, Boto3) outside the `handler` (leveraging Global Scope/Init Phase) and adjusted Lambda Timeout/Memory configurations.

### Lessons Learned:
* **"Cost-Effective Architecture" Mindset**
  * Putting Lambda inside a VPC isn't always the best practice. Learned to evaluate the trade-off between network security (Private Subnet) and cost/performance. For apps using Managed Services (DynamoDB, Bedrock), a **No-VPC** architecture is optimal to eliminate NAT Gateway costs.

* **Shifting Mindset from SQL to NoSQL**
  * Understood the core difference between normalized design (RDS) and Access Pattern-driven design (DynamoDB). Data needs to be denormalized to optimize read speeds for Real-time AI applications.

* **Monitoring as Code**
  * Monitoring/Alarm setup must occur in parallel with feature development (Dev + Ops). Learned to use Scripts/IaC instead of manual operations to manage scaling resources efficiently.