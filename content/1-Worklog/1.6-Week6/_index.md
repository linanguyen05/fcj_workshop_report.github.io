---
title: "Week 6 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

  * **Master Identity & Access Management:**
      * Shift mindset from local User management to centralized management with **IAM Identity Center**.
      * Master multi-layer security architecture via **Permission Boundary** (preventing privilege escalation) and **IAM Role Conditions** (controlling access context).
  * **Security Governance:** Understand and operate **AWS Security Hub** to automatically assess system compliance against international standards (CIS, PCI DSS).
  * **Ensure Data Safety and Recovery:** Build an automated backup strategy with **AWS Backup**, focusing on automated "Recovery Testing" mindset.

### Tasks to Implement This Week:

| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | **TOPIC: CENTRALIZED IDENTITY MANAGEMENT WITH IAM IDENTITY CENTER** <br> - **Architecture & Mechanism:** <br>  + Understand Single Sign-On (SSO) model for Multi-account environments and the role of Permission Sets. <br>  + Analyze advanced permission control models: Customer Managed Policies and Time-based Access Control. <br> - **Practice:** <br>  + **Infrastructure Setup:** Initialize AWS Organizations and activate IAM Identity Center. <br>  + **User/Group Management:** Create `Administrators` & `readOnly` groups, setup users and password policies. <br>  + **Permission & Provisioning:** Create Permission Sets (`AdministratorAccess`, `ViewOnlyAccess`) and automatically assign permissions to target accounts. <br>  + **CLI Integration:** Configure `aws configure sso` for standard OIDC authentication via command line. | 13/10/2025 | 13/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Tue | **TOPIC: PERMISSION CONTROL WITH PERMISSION BOUNDARY** <br> - **Theory & Security Mindset:** <br>  + Define "Permission Boundary" and "Effective Permissions" mechanism (Intersection between granted permissions and the boundary). <br>  + Analyze Use-cases for preventing Privilege Escalation in enterprises. <br> - **Practice:** <br>  + **Create Boundary Policy:** Write JSON policy limiting EC2 operations to Singapore Region (`ap-southeast-1`) only. <br>  + **User Configuration:** Create `ec2-admin` User granted Full Access but restricted by a Permission Boundary. <br>  + **Verification:** Verify that the User is blocked when operating in another Region (Sydney) despite having Admin permissions. | 14/10/2025 | 14/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | **TOPIC: IAM ROLE MECHANISM & ACCESS CONDITIONS** <br> - **Core Concepts:** <br>  + Distinguish Principal, Identities (User/Group/Role), and authentication mechanisms. <br>  + Master the Assume Role process and the role of AWS STS (Security Token Service). <br> - **Practice:** <br>  + **User/Group Management:** Create admin group `ec2-rds-admin` and functional users. <br>  + **Switch Role Config:** Create IAM Role, setup Trust Relationship allowing a standard User (`No-permission-user`) to perform Assume Role. <br>  + **Advanced Security:** Add Conditions to Trust Policy to restrict Switch Role rights based on Source IP address and specific Time windows. | 15/10/2025 | 15/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | **TOPIC: AUTOMATED SECURITY GOVERNANCE WITH SECURITY HUB** <br> - **Standards & Assessment:** <br>  + Research standards: CIS AWS Foundations, PCI DSS, and AWS Foundational Security Best Practices. <br>  + Understand Security Score mechanism and relation to AWS Config. <br> - **Practice:** <br>  + **Activate & Config:** Enable Security Hub, turn on standards, and configure AWS Config (Recording). <br>  + **Monitor & Tune:** Analyze Findings, perform suppression of rules unsuitable for Lab environment. <br>  + **Resource Cleanup:** Properly disable services to optimize costs. | 16/10/2025 | 16/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | **TOPIC: AUTOMATED BACKUP & RESTORE STRATEGY (AWS BACKUP)** <br> - **Backup & Restore Theory:** <br>  + Define RTO (Recovery Time Objective) and RPO (Recovery Point Objective). <br>  + AWS Backup Architecture: Backup Plan, Vault, and Notifications. <br> - **Practice:** <br>  + **Infrastructure as Code:** Use CloudFormation to deploy simulated infrastructure (EC2, Lambda, SNS). <br>  + **Backup Config:** Create Vault, setup automated Backup Plan, and assign resources via Tags. <br>  + **Automation Workflow:** Perform On-demand Backup, trigger Lambda to auto-Restore and verify data integrity immediately upon Backup completion. | 17/10/2025 | 17/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 6:

  * Shifted governance mindset from single IAM User to **centralized identity model (Identity Center)**, solving the challenge of large-scale access management (Multi-account).
  * Successfully implemented **"Defense in Depth"** strategy: Combined Permission Boundary (preventing privilege escalation) and IAM Role Conditions (IP/Time restrictions) to ensure the principle of least privilege.
  * Established an **automated security assessment system** with AWS Security Hub, applying international standards (CIS, PCI DSS) to detect configuration vulnerabilities in real-time.
  * Upgraded data protection process: Moved beyond periodic backups with AWS Backup to integrating AWS Lambda for **automated Restore Testing**.

### Challenges – Solutions:

  * **Challenge:** `ec2-admin` User, despite being granted `AdministratorAccess`, was denied access (Access Denied) when creating an Instance.
      * **Solution:** Reviewed the Permission Boundary mechanism. Realized that effective permission is the **intersection** between the Policy assigned to the user and the Boundary. Adjusted the `StringEquals` condition in the Boundary JSON file to match the current Region.
  * **Challenge:** Error when performing Switch Role from standard User to Admin Role (Trust Relationship Error).
      * **Solution:** Re-checked the Trust Relationships tab of the Role. Required declaring the exact **ARN of the User (Principal)** in the Trust Policy for AWS STS to accept the Assume Role request.
  * **Challenge:** AWS Security Hub sent too many alerts (Findings), making it difficult to filter important information.
      * **Solution:** Performed **Tuning** by changing the status of rules unsuitable for the Lab environment to `Suppressed` to reduce noise.

### Lessons Learned:

  * **Identity is the new security perimeter:**
      * In Cloud, Firewalls are not enough. Strictly controlling Identity (Who) and Permissions (What can be done) is the most critical checkpoint to protect resources.
  * **Backup must go hand-in-hand with Restore Test:**
      * A backup that has never been tested for restoration is completely meaningless. Automating the Restore process immediately after Backup is the **Gold Standard** for data availability.
  * **Context-aware Access:**
      * Instead of granting permanent rights (Long-term credentials), prioritize using IAM Roles with binding **Conditions** such as source IP address or working hours to minimize risks if credentials are leaked.
