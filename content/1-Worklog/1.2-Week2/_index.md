---
title: "Week 2 Worklog"
date: "2025-09-08"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:
  * Practice deploying basic network and compute infrastructure.
  * Deploy Amazon VPC with full architecture (Public & Private Subnets, attach Internet Gateway, configure Route Tables, Security Groups, NAT Gateway).
  * Deploy Amazon EC2 Instances (Linux & Windows), connect via SSH and RDP.
  * Practice "least privilege" security principles in Security Groups.
  * Practice deploying a Node.js User Management application on Amazon Windows Server 2022.
  * Hone AWS cost management skills and resource cleanup after each lab.

### Tasks to Implement This Week:

| Day | Task | Start Date | End Date | Source |
| :--- | :--- | :--- | :--- | :--- |
| Mon | - Review Amazon VPC theory.<br>- Research Amazon EC2 Instances theory.<br>- **Practice:**<br>  + Create VPC with CIDR 10.10.0.0/16 and configure DNS.<br>  + Create Subnets and enable Auto-assign IP for Public Subnet.<br>  + Create Internet Gateway and attach to VPC.<br>  + Create Public Route Table, configure route 0.0.0.0/0 → IGW.<br>  + Create Security Group for Public Subnet (SSH, ICMP).<br>  + Create Security Group for Private Subnet (SSH from Public SG).<br>  + Create Security Group for VPC Endpoint (Internal HTTPS). | 15/09/2025 | 15/09/2025 | |
| Tue | - Deploy Amazon EC2 Instances:<br>  + Create EC2 Instances in Public Subnet and Private Subnet.<br>  + SSH Connection: local → EC2 Public → EC2 Private (via private IP).<br>  + Work with key pairs (aws-keypair.pem/.ppk) via PuTTY, pscp, chmod 400 to connect to EC2 servers.<br>  + Test Internet ping from Public EC2 and Private EC2 instances.<br>  + Create Elastic IP and NAT Gateway in public subnet to allow instances in private subnet to connect to the internet. | 16/09/2025 | 16/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Wed | - **Practice:**<br>  + Launch EC2 Windows Server 2022.<br>  + Connect to Windows instance on AWS EC2 via RDP.<br>  + Launch Amazon Linux 2 instance.<br>  + Connect to EC2 Linux instance using MobaXterm and PuTTY. | 17/09/2025 | 17/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Thu | - Learn basic Amazon EC2 and practice basic tasks like changing configuration, creating snapshots, building custom AMIs, and accessing when key pair is lost. | 18/09/2025 | 18/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| Fri | - Learn theory on deploying AWS User Management Node.js application on Amazon Linux.<br>- **Practice:**<br>  + Install XAMPP (Apache + MySQL) on Windows Server 2022.<br>  + Create database and user table via phpMyAdmin interface.<br>  + Install Node.js + Git on Windows instance.<br>  + Clone code repo, npm init, install dependencies.<br>  + Create .env file for DB config, use Nodemon and npm start to run app and save time. | 19/09/2025 | 19/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |

### Results Achieved in Week 2:

  * Completed VPC network architecture with Subnets, IGW, Route Tables.
  * Created full SGs for Public, Private, and VPC Endpoint.
  * Private EC2 successfully pinged Internet (via NAT Gateway).
  * EC2 Linux: Deployed Public & Private EC2, successful SSH connection.
  * EC2 Windows: Launched, successful RDP connection.
  * Installed XAMPP, Node.js, successfully deployed CRUD User Management app.
  * Managed AWS costs, cleaned up resources after each lab.

### Challenges – Solutions:

  * **Challenge:** EC2 Private could not ping Internet.
      * **Solution:** Created NAT Gateway + Private Route Table.
  * **Challenge:** SSH connection error to EC2 Private.
      * **Solution:** Checked Security Group, Route Table, NAT Gateway, SSH via EC2 Public (bastion host).
  * **Challenge:** RDP Windows password/decrypt error.
      * **Solution:** IP changes every time instance stops/starts, downloaded new remote desktop file. Decrypt password using .pem key pair, re-checked port 3389 rule in SG.

### Lessons Learned:

  * Adhere to "least privilege" security principles in Security Groups configuration.
  * Understand Public vs Private Subnets, NAT Gateway mechanism.
  * Master basic operations with EC2: changing configuration, creating snapshots, building custom AMIs, accessing when key pair is lost.
  * Know how to RDP to manage Windows Server on AWS EC2 and SSH to manage Linux Server on AWS EC2.
