---
title: "Week 1 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

  * Socialize and connect with members; get accustomed to the learning environment at First Cloud Journey.
  * Understand and grasp the basic AWS services.
  * Practice the steps to initialize and configure an AWS Free Tier account.
  * Begin familiarizing with the AWS Management Console and AWS CLI.
  * Learn about Amazon VPC and basic networking components.

### Tasks to Implement This Week:

| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | - Get to know FCJ members.<br>- Read and note the rules and regulations at the internship organization. | 09/08/2025 | 09/08/2025 | |
| Tue | - Create AWS Free Tier account.<br>- Research AWS and an overview of service groups:<br>  + Compute<br>  + Storage<br>  + Networking<br>  + Database<br>  + Monitoring<br>  + Cost Management | 09/09/2025 | 09/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | - Set up MFA for root user and admin user.<br>- Familiarize with AWS Management Console (EC2, S3, RDS, Lambda, CloudWatch).<br>- Learn about AWS Budget.<br>- **Practice:**<br>  + Set up MFA (Multi-factor Authentication).<br>  + Create Admin Group and Admin User to replace root for managing AWS resources.<br>  + Create Cost Budget, Usage Budget, RI Budget, Savings Plans Budget. | 09/10/2025 | 09/10/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | - Research AWS Support and support plans:<br>  + Basic Plan<br>  + Developer Plan<br>  + Business Plan<br>  + Enterprise Plan<br>- Learn access management with IAM.<br>- **Practice:**<br>  + Create and manage IAM Groups, IAM Users.<br>  + Implement IAM Roles with temporary permissions.<br>- Learn about Elastic IP. | 09/11/2025 | 09/11/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | - Learn Amazon VPC overview.<br>- Grasp concepts: CIDR, Subnet, Route Table, Internet Gateway, NAT Gateway.<br>- Learn overview of firewalls in Amazon VPC. | 09/12/2025 | 09/12/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 1:

  * Understood what AWS is and grasped the basic service groups:
      * Compute
      * Storage
      * Networking
      * Database
  * Successfully set up a secure AWS Free Tier account with MFA and standard IAM configuration.
  * Familiarized with the AWS Management Console; know how to search, access, and use services via the web interface.
  * Know how to contact and create cases on AWS Support.
  * Understood the theoretical architecture of AWS VPC networking and the roles of basic components.

### Challenges – Solutions:

  * **Challenge:** Initial difficulty in distinguishing between the root user and IAM user.
      * **Solution:** Practiced creating an Admin Group and Admin User to replace the root user for managing AWS resources.
  * **Challenge:** Some concepts like CIDR, Subnet, Internet Gateway, NAT Gateway, RI, and Savings Plans were new.
      * **Solution:** Consulted documentation and took notes for better memorization and deeper understanding.

### Lessons Learned:

  * Do not use the root user for normal tasks to ensure AWS account safety; always enable MFA for the root user and important IAM users.
  * Proactively manage costs and set clear alert thresholds.

### Plan for Next Week:

  * Practice deploying Amazon VPC.
  * Practice deploying EC2 instances and connecting with S3.
  * Continue expanding networking knowledge with VPC Peering and Security Groups.
