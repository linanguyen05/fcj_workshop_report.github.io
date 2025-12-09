---
title: "Week 10 Worklog"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:
* Master Serverless RAG Architecture: Analyze data flows and integration mechanisms between API Gateway, AWS Lambda, and Amazon Bedrock to build scalable GenAI applications.
* Apply Data Engineering techniques for AI: Execute Semantic Chunking strategies and Metadata Schema standardization to handle multi-structured (Multi-domain) datasets.
* Deploy secure Vector Database infrastructure: Configure Amazon RDS (PostgreSQL) with the pgvector extension and establish Security Groups to ensure secure internal VPC connectivity.
* Govern and Integrate Foundation Models: Master the Model Access Request process and utilize the SDK (boto3) to effectively interact with Cohere Embed and Claude 3 Sonnet models.

### Tasks to be carried out this week:
| Day | Task | Start Date | End Date | Documentation Source |
| :--- | :--- | :--- | :--- | :--- |
| 2 | **TOPIC: RAG ARCHITECTURE DESIGN & MULTI-DOMAIN DATA PLANNING** <br>- **Theoretical Research:** <br>  + Analyze Serverless RAG architecture data flow: User Request -\> API Gateway -\> Lambda -\> Amazon Bedrock (Knowledge Base). <br>  + Design Data Schema for Multi-domain system: Integrating Astrology, Tarot, and Numerology into a unified Vector Store. <br>- **Practice:** <br>  + Environment Initialization: Setup IAM Roles for Lambda (permissions for RDS, Bedrock) and configure VPC Network. <br>  + Ingestion Planning: Define standard Metadata structure (Category, Sub-category) to optimize Filtering capabilities. | 10/11/2025 | 10/11/2025 | AWS Documentation & Project Internal Docs |
|3 | **TOPIC: DATA ENGINEERING & CODE MODULARIZATION** <br>- **Code Refactoring:** <br>  + Transform data processing code from Monolithic to Modular architecture: Separating `config_mapping.py` (Business Logic) and `run_tagger.py` (Execution). <br>- **Practice:** <br>  + Metadata Tagging: Execute script to automatically tag and classify 65 original documents (Zodiac, Planets). <br>  + Logic Debugging: Handle Edge cases in URL-to-Category mapping to ensure 100% dataset accuracy. | 11/11/2025 | 11/11/2025 | AWS Python SDK (Boto3) Docs |
| 4 | **TOPIC: SEMANTIC CHUNKING STRATEGY & DOMAIN EXPANSION** <br>- **Research:** <br>  + Compare efficacy between Fixed-size Chunking and Semantic Chunking (keyword/context-based) for spiritual domain data. <br>  + Dataset Expansion Strategy: Analyze `cards.jsonl` (Tarot) structure for system integration. <br>- **Practice:** <br>  + Data Transformation: Write scripts to standardize Tarot data into the synchronized `content` + `metadata` format used by Astrology. <br>  + Update `run_chunker.py` v2.1: Implement Regex logic and Fallback mechanisms (RecursiveSplitter) to handle complex text structures. | 12/11/2025 | 12/11/2025 | LangChain Documentation |
| 5 | **TOPIC: LAMBDA RAG DEPLOYMENT & MODEL ACCESS MANAGEMENT** <br>- **Backend Implementation (Lambda):** <br>  + Implement `get_embedding` function: Integrate **Cohere Embed v3** model for query vectorization. <br>  + Implement `query_llm` function: Integrate **Claude 3 Sonnet** model for natural language generation. <br>- **Practice & Debug:** <br>  + Troubleshoot `ValidationException`: Execute "Request Model Access" procedure for Anthropic models in the Singapore region (ap-southeast-1). <br>  + VPC Connectivity Check: Ensure Lambda within VPC can communicate with RDS (PostgreSQL) via Security Groups. | 13/11/2025 | 13/11/2025 | AWS Bedrock User Guide |
| 6 | **TOPIC: PAYLOAD OPTIMIZATION & END-TO-END SYSTEM TESTING** <br>- **API Interface Optimization:** <br>  + Redesign JSON Payload structure: Switch to Nested Objects, separating `user_profile` (birth date/time) and `input_data` to support deep personalization. <br>- **Practice:** <br>  + Setup Local Testing: Configure `curl` scripts to simulate Frontend requests calling the API Gateway. <br>  + System Test: Execute full RAG workflow testing (Ingestion -\> Retrieval -\> Generation) and verify the accuracy of the generated responses. | 14/11/2025 | 14/11/2025 | Project Technical Docs |


### Week 10 Achievements:
* **Successfully designed a Multi-domain Data Schema:** Standardized data from disparate sources (Tarot JSONL, Scraped Web) into a unified `content` + `metadata` format, establishing a solid foundation for expanding the dataset to Numerology and Horoscope.
* **Mastered Data Engineering techniques for RAG:** Successfully refactored data processing code from Monolithic to Modular architecture, while applying "Semantic Chunking" methods to significantly improve context accuracy during retrieval.
* **Deployed a complete Serverless RAG architecture:** Successfully integrated dual AI models on Amazon Bedrock: Cohere Embed v3 (Vectorization) and Claude 3 Sonnet (Generation), establishing secure connectivity with RDS PostgreSQL via VPC.
* **Optimized API Payload Design:** Upgraded the input data structure to Nested Objects, enabling the system to process User Profile information (birth date/time) in parallel for highly personalized responses.

### Challenges – Solutions:
* `ValidationException` error when invoking the Claude 3 Sonnet model via boto3 despite correct code logic
  * **Solution:** Executed the manual "Request Model Access" procedure in the Bedrock Console. It is crucial to grant specific permissions for each Model Family in the deployment Region (Singapore/ap-southeast-1).

* Incompatibility between Tarot data (structured with multiple small fields) and the Astrology Schema (long-form text)
  * **Solution:** Developed a Data Transformation (ETL) script to merge child fields (`meaning`, `love`, `career`) into a single, semantically rich `content` field before Embedding.

* Lambda Timeout when attempting to connect to the RDS Database for Vector queries
  * **Solution:** Reconfigured Security Groups. Updated the RDS Inbound Rule to accept traffic specifically from the Lambda function's Security Group ID rather than a specific IP, ensuring seamless internal VPC connectivity.

### Lessons Learned:
* **"Schema-First" Mindset in Multi-domain Systems**
  * In multi-task RAG scenarios, designing Metadata (Category, Sub-category) is more critical than Model selection. Detailed and standardized metadata directly correlates to higher noise filtering capabilities and response accuracy.

* **Chunking Quality Defines RAG Intelligence**
  * For specialized data (Spiritual/Literary), Regex-based Splitting (based on keywords/headers) is significantly more effective than fixed-character splitting. Investing time in Preprocessing yields far greater returns than attempting to refine output via Prompt Engineering.