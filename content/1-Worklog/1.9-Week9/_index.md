---
title: "Week 9 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

  * Build a complete Serverless Data Lake on S3: From Ingest, Storage, ETL to Analysis and Visualization.
  * Master Big Data processing tools: Apply AWS Glue (DataBrew, Crawler, Job) to standardize data and Amazon Athena/Redshift for analytical queries.
  * Business Intelligence (BI) Visualization: Design interactive Dashboards, apply ML Insights and Forecasts with Amazon QuickSight.
  * AWS Cost Optimization (FinOps): Master cost analysis models (Cost Explorer), Data Transfer fees, and commitment strategies (Savings Plans, Reserved Instances).

### Tasks to Implement This Week:

| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | **TOPIC: BUILDING DATA LAKE ON S3 & DATA PREPARATION** <br>- **Foundation & Architecture:** <br>  + Understand the role of Amazon S3 as a Central Data Lake and the importance of UTF-8 Encoding. <br>  + Master AWS Glue DataBrew (Data Profiling, Recipe) for no-code data cleaning. <br>  + Distinguish row storage (CSV) vs. columnar storage (Parquet) for query optimization. <br>- **Practice:** <br>  + Environment Setup: Initialize Cloud9, install `enca` tool, upload Raw Data to S3. <br>  + Data Preparation: Configure DataBrew Project to profile, clean, and standardize Airbnb data. <br>  + Catalog & ETL: Run Glue Crawler to create Metadata and execute Glue Job to convert CSV to Parquet. | 03/11/2025 | 03/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | **TOPIC: BUILDING DATA ANALYTICS PIPELINE (INGEST-TRANSFORM-ANALYZE)** <br>- **End-to-End Analytics Architecture:** <br>  + Data flow process: Kinesis (Ingest) -\> S3 (Store) -\> Glue/EMR (Transform) -\> Athena/Redshift (Analyze). <br>  + Compare ETL methods: Glue Studio (Visual), Glue Notebook (Code), and DataBrew. <br>  + Data Warehouse (Redshift) and Serverless Serving (Lambda) architecture. <br>- **Practice:** <br>  + Streaming Data: Configure Kinesis Firehose to load simulated data (KDG) into S3 in real-time. <br>  + ETL Processing: Use Glue Studio to Join tables and Glue Notebook (PySpark) to process complex data. <br>  + Real-time & Warehousing: Run Flink SQL on Kinesis Analytics and load data into Redshift Cluster. | 04/11/2025 | 04/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | **TOPIC: DATA VISUALIZATION WITH AMAZON QUICKSIGHT** <br>- **Dashboard Design & Serverless BI:** <br>  + SPICE mechanism (in-memory engine) and QuickSight Auto-scaling model. <br>  + Core concepts: Dataset, Analysis, Dashboard, and Sheet/Theme principles. <br>- **Practice:** <br>  + Building Visuals: Connect to Athena, create KPI charts, Line Charts, Donut Charts for Sales data. <br>  + Advanced Features: Apply ML Insights to create Forecasts and Drill-down into detailed data. <br>  + Interactivity: Set up Cascading Filters, Navigation Actions, and Publish reports. | 05/11/2025 | 05/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | **TOPIC: MONITORING & COST MANAGEMENT WITH COST EXPLORER** <br>- **Cloud Financial Management Principles:** <br>  + Overview of AWS Cost Explorer and Tagging strategy (Cost Allocation Tags). <br>  + Understand Data Transfer pricing model: Inbound (Free), Outbound, and especially Inter-AZ/Inter-Region fees. <br>- **Practice:** <br>  + Resource Analysis: Activate Cost Explorer, filter costs by Service (EC2) and Tag to find budget hotspots. <br>  + Audit Data Transfer: Analyze Outbound data transfer costs and communication between AZs. <br>  + Reporting: Create and save Custom Reports for monthly cost tracking. | 06/11/2025 | 06/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | **TOPIC: COST OPTIMIZATION STRATEGY (SAVINGS PLANS & RI)** <br>- **Commitment Models:** <br>  + Distinguish Savings Plans (Flexible, applicable to Fargate/Lambda) and Reserved Instances (Traditional). <br>  + Compare EC2 Instance Savings Plans (Deep) vs Compute Savings Plans (Broad). <br>  + Specifics of Reserved DB Instances for RDS (Engine/Class binding). <br>- **Practice:** <br>  + Purchasing Process: Navigate Console to view Recommendations and execute Savings Plans/RI Purchase. <br>  + Lifecycle Management: Learn how to use Marketplace to buy/sell RIs and Order Queueing techniques. <br>  + Summary & Cleanup of all Lab resources. | 07/11/2025 | 07/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 9:

  * **Successfully Built Serverless Data Lake Architecture on S3:** Understood and implemented data layering process (Raw -\> Cleaned -\> Curated). Grasped the importance of checking Encoding (UTF-8) using `enca` tool on Cloud9 before ingesting data.
  * **Mastered ETL Process and Query Optimization:**
      * Flexibly applied 3 ETL methods: **AWS Glue DataBrew** (No-code cleaning), **Glue Studio** (Visual Join), and **Glue Notebook** (PySpark scripting).
      * Proved the efficiency of **Parquet** (Columnar) format over CSV: reduced storage size, increased Athena query speed, and reduced data scan costs by multiple times.
  * **Deployed Real-time Analytics & Visualization Pipeline:**
      * Successfully configured **Kinesis Firehose** to load simulated data streams into S3.
      * Built interactive Dashboards on **Amazon QuickSight**, utilizing **SPICE** memory and ML Insights features (Forecast, Anomaly Detection).
  * **Mastered Governance & Cost Optimization Strategies (FinOps):**
      * Used **Cost Explorer** to inspect costs at the Resource level and detect waste from Data Transfer fees (Inter-AZ).
      * Clearly distinguished commitment package thinking: Prioritize **Compute Savings Plans** for flexibility (Compute/Lambda/Fargate) and **Reserved Instances** when needing deep discounts for stable infrastructure (RDS/EC2).

### Challenges – Solutions:

  * **Challenge:** Strange characters displayed when Crawler scanned Raw Data.
      * **Solution:** Original data from multiple sources often has incorrect character encoding. Needed to use `enca -L none` command on Linux environment (Cloud9) to detect and convert all files to standard UTF-8 before uploading to S3.
  * **Challenge:** Abnormally high Data Transfer costs even without downloading data to the Internet.
      * **Solution:** Re-checked network architecture. Detected traffic communication between EC2 Instances located in different Availability Zones (Inter-AZ Data Transfer). The solution was to replan resources into the same AZ if strict HA is not required, or use VPC Endpoints for S3 to keep traffic within the internal AWS network.
  * **Challenge:** Athena scanned too much data causing slowness and high costs.
      * **Solution:** Instead of querying CSV files directly (scanning the entire file), converted data to **Parquet** format combined with **Partitioning** planning (folder partitioning by time). Resulted in reducing scanned data volume to only 1/10th.

### Lessons Learned:

  * **Format:** In Big Data, *how* you store is more important than *where* you store. Converting to columnar formats (**Parquet/ORC**) and **Partitioning** strategies are mandatory techniques to ensure performance and low costs.
  * **Tagging is the backbone of FinOps:** Cost Explorer becomes useless if resources lack **Tags**. Must establish discipline for tagging `Project`, `Environment`, `Owner` right from resource creation to make the financial picture transparent.
  * **Smart Commitment Strategy:** Don't rush to buy Reserved Instances (RI) if unsure about long-term architecture. **Compute Savings Plans** are a safer choice as they act like a "comprehensive plan" (allowing switches from EC2 to Lambda/Fargate), whereas RI is like a "fixed table reservation" (hard to change).
