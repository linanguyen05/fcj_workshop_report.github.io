---
title: "Event 4"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

### AWS Cloud Mastery Series #2: Workshop DevOps on AWS

### Event Purpose

This workshop was designed to bridge the gap between DevOps theory and real-world implementation on the Cloud. Beyond introducing tools, the event focused on building system thinking, helping attendees grasp the standard workflow from Development to Operations. The core objective was to master key AWS services to build effective CI/CD pipelines, manage Infrastructure as Code (IaC), operate containers, and establish comprehensive Observability.

### Program Overview

The program provided a holistic view of the skill development roadmap on AWS:

  - **Certification Roadmap:** Analyzed the career progression path through certifications such as *AWS Certified Solutions Architect* (Architecture), *SysOps Administrator* (Operations), and the advanced *AWS Certified DevOps Engineer – Professional*.
  - **Next Steps:** Provided an ecosystem of resources including hands-on labs, whitepapers, and community support to maintain learning momentum after the event.

### Key Highlights

Under the guidance of AWS experts, the workshop delved into critical technical aspects:

  - **End-to-End CI/CD Pipeline:** Explored how **AWS CodePipeline** acts as the "backbone" to automate the software release process. It integrates everything from source control (CodeCommit/GitHub) and build (CodeBuild) to deployment (CodeDeploy), ensuring consistency across environments.
  - **Infrastructure as Code (IaC):** Compared and applied two approaches: **AWS CloudFormation** (defining infrastructure via JSON/YAML) and **AWS CDK** (Cloud Development Kit - defining infrastructure using familiar programming languages like TS/Python). CDK was particularly impressive for its superior Developer Experience (DX).
  - **Container Ecosystem:** Analyzed options based on real-world use cases: **Amazon ECS** for simplicity and native AWS integration; **Amazon EKS** for complex systems using Kubernetes; and **AWS App Runner** for web apps needing rapid deployment without infrastructure management.
  - **Observability:** Went beyond basic "monitoring." Combined **Amazon CloudWatch** (logs, metrics collection) and **AWS X-Ray** (distributed tracing) to gain deep insights into application health and end-user experience.
  - **Culture & Best Practices:** Emphasized that tools are just the means. Success comes from applying *Feature Flags* to reduce deployment risk, rigorous *Automated Testing* strategies, and transparent *Incident Management*.

### What I Learned

  - **"Culture First" Mindset:** I realized the biggest barrier to DevOps isn't technology but resistance to change. A successful DevOps team requires close collaboration and shared responsibility.
  - **The Power of Automation:** Automating the pipeline not only increases release velocity but also ensures reliability, eliminating errors caused by manual human intervention.
  - **IaC is "Version Control" for Infrastructure:** Treating infrastructure as source code allows the team to review, audit, and roll back environments quickly in case of incidents, effectively solving the "configuration drift" problem.
  - **Container Strategy:** There is no "one-size-fits-all" solution. Choosing between ECS or EKS depends heavily on the operations team's size and the project's specific requirements.
  - **The Importance of Tracing:** In microservices architecture, without distributed tracing (like X-Ray), finding the root cause of latency issues is like looking for a needle in a haystack.

### Application to Work

Based on the knowledge acquired, I plan to apply the following to my current internship project:

  - **Implement CI/CD Pipeline:** Propose a transition from the current manual deployment process to using AWS CodePipeline for automating code pushes to the Staging environment.
  - **Adopt IaC:** Start writing simple CloudFormation or CDK scripts to provision environments instead of relying on "ClickOps" (manual console clicks), making project handover easier in the future.
  - **Evaluate Containerization:** Research dockerizing specific project modules and test deploying them on AWS App Runner to evaluate performance.
  - **Optimize Monitoring:** Configure additional CloudWatch Alarms to send immediate alerts via SNS/Email when CPU or Memory exceeds thresholds, rather than waiting for system failure to notice.

### Personal Experience & Key Takeaways

Before attending this workshop, the concept of DevOps was quite vague to me, often confused with just using Docker or Jenkins. However, this session truly shifted my mindset:

**1. A Sense of Process Control:**
Watching the "Succeeded" status turn green on CodePipeline, running automatically from code commit to production update, was incredibly satisfying. It helped me understand that a Developer's job isn't just writing code, but ensuring that code runs successfully in the real world.

**2. X-Ray Vision:**
The hands-on session on Observability with AWS X-Ray was the highlight. It felt like giving the application an X-ray scan; I could see exactly where requests were bottlenecked in the database or API. This eliminates the "guessing game" when debugging.

**3. Core Lessons:**

  - **Automation is Key:** The principle "If you have to do it manually more than twice, automate it" will be my guideline.
  - **DevOps is a Shared Responsibility:** Understanding operations helps me write "cloud-native" code that is friendlier to the system, easier to deploy, and easier to scale.
  - **Measure Everything:** You cannot improve what you cannot measure. Metrics and Logs must be treated with the same importance as product features from Day 1.

