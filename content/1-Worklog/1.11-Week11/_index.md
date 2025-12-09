---
title: "Week 11 Worklog"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:
* Deeply understand and apply "Semantic Chunking" techniques to standardize and optimize input data for multi-domain RAG systems (Astrology, Tarot).
* Master the Serverless infrastructure deployment process: Configure AWS Lambda within a VPC environment, setup IAM Roles and Security Groups for secure connectivity to Amazon RDS and Amazon Bedrock.
* Design and deploy standard RESTful APIs on Amazon API Gateway using POST methods to handle complex payload structures (Nested JSON) for personalization features.

### Tasks to be carried out this week:
| Day | Work Content | Start Date | End Date | Resources |
| :--- | :--- | :--- | :--- | :--- |
| 2 | **TOPIC: RAG MULTI-DOMAIN ARCHITECTURE & DATA STANDARDIZATION** <br>- **Architecture Research:** <br>  + Analyze data flow for a multi-domain RAG system (Astrology, Tarot, Numerology). <br>  + Evaluate Vector Store solutions: Select RDS (PostgreSQL with pgvector) over DynamoDB to optimize relational queries combined with vector search. <br>- **Practice:** <br>  + **Code Refactoring:** Re-architect Python source code from Monolithic to Modular structure (`config_mapping.py`, `run_tagger.py`) for better maintainability. <br>  + **Schema Design:** Unify input data format (`content` + `metadata`) for both Tarot and Astrology datasets. | 17/11/2025 | 17/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 3 | **TOPIC: DATA ENGINEERING & SEMANTIC CHUNKING TECHNIQUE** <br>- **Advanced Data Processing:** <br>  + Finalize `run_chunker.py` script (v2.1): Integrate Regex (`re.IGNORECASE`) to identify entities (Zodiac, Planets) as semantic split points. <br>  + NLP Processing: Implement `slugify` function to normalize Vietnamese Metadata (remove accents, standardize format) for precise search. <br>- **Practice:** <br>  + Execute "Metadata Tagging" to classify documents into categories (Zodiac, Planets). <br>  + Perform "Semantic Chunking" and debug logic errors in URL-to-Category mapping. | 18/11/2025 | 18/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 4 | **TOPIC: INFRASTRUCTURE - LAMBDA IN VPC & BEDROCK SECURITY** <br>- **AWS Network Concepts:** <br>  + Understand Lambda routing within a VPC and connectivity to RDS located in a different Availability Zone (Multi-AZ). <br>  + Configure Security Group Rules to allow traffic from Lambda to Database. <br>- **Practice:** <br>  + Deploy Lambda `metaphysicalAPI`: Configure VPC, Subnet (Public-b), and IAM Role for Bedrock access. <br>  + AI Model Management: Perform "Request Access" for Claude 3 Sonnet and Cohere Embed models in the Singapore region to resolve `ValidationException`. | 19/11/2025 | 19/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 5 | **TOPIC: RESTFUL API DESIGN & COMPLEX PAYLOAD STRUCTURE** <br>- **API Gateway Design:** <br>  + Initialize REST API (`Metaphysical-Gateway`) with Regional Endpoint Type. <br>  + Define `/metaphysical` Resource and **POST** Method to secure user data. <br>- **Practice:** <br>  + Construct JSON Payload: Design Nested Objects containing `user_context` (birth date, time, place) and `feature_type` to serve response personalization. <br>  + Configure Integration Request to forward data to Lambda function. | 20/11/2025 | 20/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| 6 | **TOPIC: SYSTEM INTEGRATION & END-TO-END TESTING** <br>- **Configuration & Security:** <br>  + Enable CORS (Cross-Origin Resource Sharing) on API Gateway to allow Frontend requests. <br>  + Audit IAM Permissions (Least Privilege principle) for Lambda, Bedrock, and RDS services. <br>- **Practice:** <br>  + **Local Testing:** Setup local environment, utilize `curl` and Postman to simulate requests. <br>  + **End-to-End Test:** Verify the complete data flow from API -\> Lambda -\> Bedrock -\> Correct JSON Response structure. | 21/11/2025 | 21/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Week 11 Achievements:
* **Finalized Multi-domain RAG Data Pipeline:**
    * Successfully resolved complex data fragmentation issues using **"Semantic Chunking"**. Instead of mechanical fixed-length splitting, the system now automatically identifies entities (Planets, Zodiacs) to segment text precisely.
    * Standardized the input Data Schema (`content` + `metadata`) for both Tarot and Astrology tasks, laying the foundation for future Numerology expansion.
* **Deployed Serverless Infrastructure for AI Integration:**
    * Successfully built a RESTful API on Amazon API Gateway, tightly integrated with AWS Lambda as the backend for logic orchestration.
    * Configured secure connectivity between Lambda (in Public Subnet) and RDS Database (in Private Subnet) for Vector storage.
* **Code Optimization (Refactoring):** Transformed the entire data processing source code from a Monolithic structure to a Modular architecture (`config_mapping.py`, `run_chunker.py`), significantly improving readability, debugging capabilities, and maintainability.

### Challenges – Solutions:
* **`ValidationException` error when invoking Anthropic Claude 3 model on Bedrock**
    * **Root Cause:** AWS does not grant default access to third-party models (like Anthropic or Cohere) upon account creation.
    * **Solution:** Accessed the Bedrock Console, navigated to "Model access," selected the Singapore Region, and manually performed "Request access" for specific models (Claude 3 Sonnet, Cohere Embed).
* **Lambda Timeout when attempting to connect to RDS**
    * **Root Cause:** Although Lambda was deployed within the VPC, the RDS Security Group did not allow inbound traffic from the Lambda function.
    * **Solution:** Instead of opening Public IPs (which is insecure), configured the RDS Security Group to accept Inbound Rules specifically from the **Lambda's Security Group ID**. This established a secure internal "Chain of trust."
* **Accented Vietnamese Metadata caused Filtering/Search inaccuracies**
    * **Solution:** Developed a `slugify` utility function (utilizing the `unicodedata` library) to normalize all Metadata into an unaccented, lowercase, and hyphenated format (e.g., "Bạch Dương" -> "bach-duong"), ensuring absolute precision for OpenSearch/Postgres queries.

### Lessons Learned:
* **Data Quality determines AI Quality (Garbage In, Garbage Out)**
    * RAG implementation success relies not just on high-end Models, but heavily on **Data Preparation**. Investing time in Regex logic for Semantic Chunking yields significantly higher search efficiency and relevance compared to standard fixed-size chunking.
* **API Design Mindset (RESTful Design)**
    * For complex payloads containing sensitive user context (`user_context`), using the **POST** method is mandatory. This ensures better security and data extensibility compared to forcing complex objects into GET URL parameters.
* **VPC Networking Mechanism**
    * Gained a deep understanding that resources within the same VPC (even across different Subnets or Availability Zones) can communicate seamlessly if Route Tables and Security Groups are correctly configured. Co-location in the same AZ is not a strict requirement for connectivity, though it may affect latency slightly.