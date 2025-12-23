<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Shane Brown  
**Email:** shanebrown848@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you create a logically isolated virtual network inside the AWS Cloud where you can launch and manage AWS resources such as EC2 instances. It is useful because it gives you full control over your network configuration, including IP address ranges, subnets, routing, and security, allowing you to securely control how resources communicate with each other and with the internet.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create isolated virtual networks, launch EC2 instances inside those networks, and control how traffic flows between them. I configured VPC settings like CIDR blocks, subnets, route tables, and security rules, then used VPC peering and VPC Flow Logs to test connectivity and monitor network traffic between resources.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how much insight VPC Flow Logs provide into network activity. Seeing exactly which traffic was accepted or rejected, along with source and destination IPs, protocols, and byte counts, made it much clearer how routing and security rules actually affect real network traffic.

### This project took me...

This project took me about an hour and 15 mins.

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will create two Amazon VPCs from scratch using the VPC creation wizard. I am doing this to quickly set up the network environments needed for monitoring and to revisit how multiple VPCs are structured before adding VPC peering and flow logs in later steps.

### Step 2 - Launch EC2 instances

In this step, I will launch an EC2 instance in each VPC because these instances will generate network traffic that can be monitored and analyzed later. Creating EC2 instances in both VPCs also allows me to test connectivity, VPC peering, and verify that network monitoring tools like VPC Flow Logs are capturing real traffic.

### Step 3 - Set up Logs

In this step, I will set up VPC Flow Logs to capture and record all inbound and outbound network traffic in my VPCs. I am doing this to store detailed traffic data in a central location so I can monitor, analyze, and troubleshoot network activity using tools like Amazon CloudWatch in the next steps.

### Step 4 - Set IAM permissions for Logs

In this step, I will create and assign an IAM role with the correct permissions so VPC Flow Logs can write log data and send it to Amazon CloudWatch. I am doing this because Flow Logs need explicit permission to deliver network traffic records to a CloudWatch log group, and setting up this role completes the flow log configuration for monitoring my VPC traffic.

---

## Multi-VPC Architecture

I started my project by launching two Amazon VPCs using the VPC creation wizard. Each VPC was created with a single Availability Zone and one public subnet, and no private subnets. In total, I created two VPCs and two public subnets, one subnet in each VPC, to prepare the environment for monitoring and peering in later steps.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because each VPC must use a non-overlapping IP address range to avoid routing conflicts. Unique CIDR blocks ensure that traffic can be correctly routed between VPCs and make features like VPC peering and network monitoring work as expected.

### I also launched EC2 instances in each subnet

My EC2 instances’ security groups allow All ICMP – IPv4 traffic from 0.0.0.0/0. This is because I needed to run ping tests between instances and across VPCs to generate network traffic and validate connectivity. Allowing ICMP from all IP addresses ensured that the ping tests would succeed and that there would be enough traffic for monitoring with VPC Flow Logs later in the project.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are records that capture events and activities happening within a system or application. They store information such as network traffic, user actions, system operations, and errors, which helps engineers monitor performance, troubleshoot issues, and understand what is happening inside their infrastructure.

Log groups are containers in Amazon CloudWatch that organize and store related log data together. They act like folders that group logs from the same source, service, or application, making it easier to manage, search, and analyze logs within a specific AWS region.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy because VPC Flow Logs do not have permission by default to write log data to Amazon CloudWatch. This policy grants the required permissions to create log groups and log streams and to send log events, allowing Flow Logs to successfully store network traffic logs in CloudWatch for monitoring and analysis.

I created an IAM role so VPC Flow Logs could assume that role and gain permission to write network traffic logs to Amazon CloudWatch. The role uses a custom trust policy that explicitly allows only the VPC Flow Logs service to use it, while the attached IAM policy defines what actions are allowed, such as creating log groups, log streams, and sending log events. This separation improves security by ensuring only the intended AWS service can use the permissions.

A custom trust policy is a policy that defines who is allowed to assume an IAM role. It specifies which AWS service, user, or role can use the role, rather than what actions the role can perform. In this project, the custom trust policy ensures that only VPC Flow Logs is allowed to assume the role, which helps keep permissions tightly controlled and secure.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will generate network traffic by sending messages from the EC2 instance in VPC 1 to the EC2 instance in VPC 2. I am doing this to create traffic that can be captured by VPC Flow Logs and to confirm that the VPC peering connection is working correctly while monitoring the network activity.

### Step 6 - Set up a peering connection

In this step, I will create a VPC peering connection between VPC 1 and VPC 2 so the two networks can communicate directly using their private IP addresses. I am doing this to fix the connectivity issue from the ping test and to enable private traffic flow between the VPCs, which we can then monitor using VPC Flow Logs.

### Step 7 - Analyze flow logs

In this step, I will review the VPC Flow Logs that were captured for VPC 1’s public subnet and analyze the recorded traffic. I am doing this to confirm the flow logs are successfully collecting network activity and to use CloudWatch Log Insights to identify what traffic was accepted or rejected during our connectivity tests.

---

## Connectivity troubleshooting

The ping did not receive any replies, which means Instance 1 was able to send traffic, but Instance 2 was not responding. This indicated that there was still a connectivity issue between the two VPCs. Even though ICMP traffic was allowed in the security group, the problem was likely related to routing or the VPC peering configuration, which needed to be reviewed to ensure traffic could flow correctly between both VPCs.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance’s public IP address, which means the two EC2 instances can successfully communicate over the public internet. This confirms that the instance is reachable, its security group allows ICMP traffic, and internet connectivity is working correctly. It also shows that the issue is not with the instance itself, but with private network routing or VPC peering when using private IP addresses.

---

## Connectivity troubleshooting

Looking at VPC 1’s route table, I identified that the ping test with Instance 2’s private address failed because there was no route that directed traffic for VPC 2’s CIDR block to the VPC peering connection. Without this specific route, traffic to the private IP could not use the peering link and instead had no valid path for private communication, causing the ping to fail.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs’ route tables so that traffic between VPC 1 and VPC 2 knows how to reach each other using the VPC peering connection. Without these routes, even though the peering connection exists, the VPCs would not know where to send traffic destined for the other VPC’s private IP range. Adding these routes allows private network traffic to flow directly between the two VPCs instead of going through the public internet.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2’s private IP address. This means the VPC peering connection is working correctly, the route tables are properly configured, and traffic can now flow directly between VPC 1 and VPC 2 using their private IP addresses without going through the public internet.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about the details of network traffic moving in and out of our VPC resources. Each flow log record includes information such as the source IP address, destination IP address, source and destination ports, the protocol used (like TCP or ICMP), the number of packets and bytes transferred, the time the traffic was recorded, and whether the traffic was accepted or rejected by the network settings. Together, these details help us understand who is communicating with our resources, how the traffic is flowing, and whether security rules are allowing or blocking that traffic.

For example, the flow log I’ve captured tells us that network traffic was sent from a specific source IP address to my EC2 instance, including how much data was transferred, which protocol and port were used, and whether the traffic was accepted or rejected. It shows when the traffic occurred, how many packets were involved, and confirms whether my security groups and network ACLs allowed or blocked that connection.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is a CloudWatch feature that lets you analyze and explore log data by running queries against it. It allows you to filter, sort, and aggregate logs to uncover patterns, identify high-traffic sources and destinations, troubleshoot connectivity issues, and gain insights into how your network and resources are behaving over time.

I ran the “Top 10 byte transfers by source and destination IP addresses” query. This query analyzes my VPC Flow Logs to identify which pairs of source and destination IP addresses transferred the most data. It helps highlight the busiest network traffic paths in my VPC, making it easier to see where the largest data flows are happening and spot heavy or unusual network activity.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-monitoring_3e1e79a1)

---

---
