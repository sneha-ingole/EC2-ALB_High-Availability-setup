🚀 EC2-ALB_High-Availability-setup
📌 Project Overview

This project demonstrates how to design and implement a fault-tolerant and highly available web architecture using:

Amazon EC2 (2 Web Servers)

Application Load Balancer (ALB)

Target Groups

Multi-AZ Deployment

The Application Load Balancer distributes incoming traffic between two EC2 instances to ensure high availability and reliability.

🏗️ Architecture
                Internet
                    |
          ---------------------
          | Application Load  |
          |     Balancer      |
          ---------------------
             |              |
        -----------      -----------
        | Server A |      | Server B |
        -----------      -----------


Server A → Hosted in AZ-1

Server B → Hosted in AZ-2

ALB distributes traffic across both

🛠️ Services Used

AWS EC2

Application Load Balancer (ALB)

Target Group

Security Groups

VPC with Public Subnets

⚙️ Step 1: Launch EC2 Instances

Launch 2 EC2 instances in different Availability Zones.

Configuration:

AMI: Amazon Linux 2

Instance Type: t2.micro (Free Tier)

Allow:

SSH (22)

HTTP (80)

💻 User Data Script (Server A)
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd

echo "<h1>Server A</h1>" > /var/www/html/index.html

💻 User Data Script (Server B)# EC2-ALB_High-Availability-setup

#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd

echo "<h1>Server B</h1>" > /var/www/html/index.html
⚖️ Step 2: Create Target Group
Go to EC2 → Target Groups

Click Create Target Group

Choose:

Target Type: Instances

Protocol: HTTP

Port: 80

Register both EC2 instances

Create Target Group

🌐 Step 3: Create Application Load Balancer
Go to EC2 → Load Balancers

Click Create Load Balancer

Choose Application Load Balancer

Scheme: Internet-facing

Select at least 2 public subnets

Attach Security Group allowing HTTP (80)

Select the Target Group

Create Load Balancer

🧪 Testing the Architecture
Copy the ALB DNS name

Paste in browser

Refresh multiple times

You should see:

“Server A”

“Server B”

Traffic is distributed between both servers.

✅ Expected Outcome
High Availability

Load Balanced Traffic

Fault Tolerance (if one server stops, traffic goes to the other)

💡 Key Concepts Demonstrated
Multi-AZ deployment

Load balancing

Target group health checks

Auto traffic distribution

Scalable architecture design

