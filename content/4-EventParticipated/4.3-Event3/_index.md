---
title: "Event 3"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

### AWS Cloud Mastery Series #1: Workshop AI/ML/GenAI on AWS

### Event Purpose

This workshop was organized to bridge the gap between Machine Learning (ML) theory and practical enterprise applications. The core focus was to equip attendees with a "Cloud-native" mindset when building AI solutions: from standardizing traditional ML workflows (MLOps) with **Amazon SageMaker** to embracing the Generative AI (GenAI) wave via **Amazon Bedrock**. The ultimate goal was to help developers understand how to integrate Large Language Models (LLMs) into applications securely, reliably, and cost-effectively.

### Program Overview

#### 8:30 – 9:00 | Welcome & The Big Picture

  - Check-in and networking with AWS engineers and the developer community.
  - Introduction to the workshop roadmap and problem-solving mindset using AI.
  - Updates on AI/ML trends in the Vietnamese market: Opportunities and challenges for young talent.

#### 9:00 – 10:30 | Deep Dive: Traditional ML Ecosystem on AWS

**Amazon SageMaker – From Raw Data to Production:**

  - **Data Engineering:** Approaches to using tools like SageMaker Data Wrangler for low-code data cleaning and visualization, combined with Ground Truth for automated data labeling.
  - **Training & Tuning:** Understanding how SageMaker manages training infrastructure (instance management), leveraging Spot Instances for cost savings, and using Automatic Model Tuning to find optimal hyperparameters.
  - **MLOps Best Practices:** Getting acquainted with SageMaker Pipelines and Model Registry to manage the model lifecycle, ensuring reproducibility, and automating CI/CD workflows for ML.

**Live Demo: SageMaker Studio Experience**
A demonstration showcasing the power of SageMaker Studio's "Single Pane of Glass," allowing developers to seamlessly switch between coding in Notebooks, tracking experiments, and deploying endpoints with just a few clicks.

#### 10:45 – 12:00 | The Era of Generative AI with Amazon Bedrock

**Foundation Models (FMs) – The Power of Choice:**

  - Approaching "Serverless GenAI": Accessing top-tier models (Claude 3.5 Sonnet, Llama 3, Amazon Titan) via a single API without server management.
  - Model Selection Strategy: Balancing Intelligence, Latency, and Cost.

**Advanced Prompt Engineering & Reasoning:**

  - **Zero-shot vs. Few-shot:** Techniques for providing examples to guide model responses.
  - **Chain-of-Thought (CoT):** Breaking down complex problems to enhance logical reasoning, particularly useful for math or business logic tasks.

**RAG (Retrieval-Augmented Generation) & Knowledge Bases:**

  - Solving LLM "hallucinations" and outdated data issues using RAG architecture.
  - Hands-on integration of Knowledge Base for Amazon Bedrock: Automating the vectorization process from S3 to Vector Stores (e.g., OpenSearch Serverless).

**Agents & Guardrails – Building Smart & Safe Applications:**

  - **Agents:** Enabling AI to perform actions (call APIs, query databases) rather than just generating text.
  - **Guardrails:** Establishing safety barriers to filter toxic, sensitive content, or ensure compliance with enterprise policies (PII redaction).

**Live Demo: Enterprise Virtual Assistant**
Building an internal chatbot capable of looking up company policy documents (via RAG) while refusing to answer sensitive financial questions (thanks to Guardrails).

### Highlights

  - **Unified Platform:** SageMaker is not just a training tool but a complete end-to-end MLOps ecosystem.
  - **Democratizing GenAI:** Amazon Bedrock makes advanced AI models accessible via a simple API.
  - **The Power of RAG:** The "golden key" to incorporating proprietary data into AI without expensive model fine-tuning.
  - **Responsible AI:** Data safety and content control (Guardrails) are non-negotiable elements for real-world deployment.

### What I Learned

  - **Infrastructure Mindset:** Understood the massive difference between running models locally versus on the Cloud with scalable capabilities.
  - **Context is King:** In GenAI, Prompt Engineering skills and providing the right context (via RAG) are often more critical than tweaking model weights.
  - **Automated Workflows:** SageMaker Studio minimizes manual tasks, allowing developers to focus on algorithmic logic.
  - **Security by Design:** Integrating Guardrails from the design phase helps avoid legal and brand risks later.

### Application to Work

  - **Data Analysis:** Propose using SageMaker Studio Lab for small-scale data analysis tasks within the company or personal projects.
  - **RAG Implementation:** Build an Internal Search Tool for the team's technical documentation using Amazon Bedrock and Knowledge Base.
  - **Process Optimization:** Research using Bedrock Agents to automate repetitive tasks like weekly report summarization or invoice information extraction.
  - **Standardizing Prompts:** Develop a standard Prompt Template library for the team to ensure consistent AI output quality.

### Personal Experience

This was truly an eye-opening workshop for an intern like me. Previously, terms like RAG or Vector Database were quite abstract in theory, but interacting directly with the Amazon Bedrock console made everything much clearer and more logical.

  - I was particularly impressed by the deployment speed: it took only about 30 minutes to set up a chatbot that could understand my own PDF documents—something that would take days to code manually.
  - The intuitive interface of SageMaker Studio made me less "intimidated" by the idea of managing ML infrastructure.
  - Most importantly, I realized that in the AI era, "question-asking" skills (Prompting) and System Design thinking are becoming just as important as pure coding skills.

### Key Takeaways

  - **Data is Fuel, AI is the Engine:** For the engine to run smoothly, input data (for RAG or Training) must be clean and well-organized.
  - **Don't Reinvent the Wheel:** Leveraging Managed Services like Bedrock or SageMaker accelerates development significantly compared to building infrastructure from scratch.
  - **AI Won't Replace Humans, But Those Who Use AI Will Replace Those Who Don't:** Proficiency in tools like Bedrock is a massive competitive advantage in today's job market.