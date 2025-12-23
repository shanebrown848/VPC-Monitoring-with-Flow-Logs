# VPC Monitoring with Flow Logs

**Project Link:** https://learn.nextwork.org/projects/aws-networks-monitoring  
**Author:** Shane Brown  

---

## Overview

This project focuses on monitoring and analyzing network traffic within Amazon Virtual Private Clouds (VPCs) using VPC Flow Logs. The goal is to gain visibility into how traffic moves through cloud networks and how routing, peering, and security rules affect real network behavior.

This project introduces monitoring as a critical layer in cloud networking and security operations. :contentReference[oaicite:0]{index=0}

---

## What I built

I configured network monitoring for a multi-VPC environment and analyzed traffic using AWS logging tools. This included:

- Creating multiple VPCs with unique CIDR blocks  
- Launching EC2 instances to generate network traffic  
- Enabling VPC Flow Logs at the VPC level  
- Sending flow logs to Amazon CloudWatch  
- Creating IAM roles and policies for log delivery  
- Testing connectivity and generating monitored traffic  

This setup reflects how cloud teams monitor, audit, and troubleshoot network activity in production environments. :contentReference[oaicite:1]{index=1}

---

## Key concepts learned

- What VPC Flow Logs capture and why they matter  
- How network traffic is accepted or rejected by routing and security rules  
- How IAM roles and trust policies enable service-to-service logging  
- How CloudWatch log groups organize network logs  
- How VPC peering and routing affect private traffic flow  
- How monitoring improves visibility and security posture :contentReference[oaicite:2]{index=2}

---

## Monitoring network traffic

VPC Flow Logs record metadata about network traffic flowing in and out of VPC resources. Each record includes information such as:

- Source and destination IP addresses  
- Protocol and port numbers  
- Packet and byte counts  
- Whether traffic was accepted or rejected  

These logs make it possible to see exactly how traffic behaves inside cloud networks. :contentReference[oaicite:3]{index=3}

---

## Testing and troubleshooting

I generated traffic using `ping` between EC2 instances and observed how traffic behaved before and after configuring VPC peering and route tables.

- Failed pings revealed missing routes or peering issues  
- Successful pings confirmed private connectivity  
- Flow logs showed which traffic was accepted or rejected  

This process demonstrated how monitoring tools support effective troubleshooting. :contentReference[oaicite:4]{index=4}

---

## Analyzing flow logs

I used CloudWatch Logs Insights to query VPC Flow Logs and identify traffic patterns. Queries such as top source and destination IPs by data transfer helped highlight where the most network activity occurred.

Log analysis provides actionable insight for performance tuning, security monitoring, and incident investigation. :contentReference[oaicite:5]{index=5}

---

## Why this project matters

Network monitoring is essential for maintaining secure and reliable cloud infrastructure. Without visibility into traffic flow, misconfigurations and security risks can go undetected.

This project demonstrates how AWS provides built-in tools to observe, analyze, and troubleshoot cloud network activity in a structured and scalable way. :contentReference[oaicite:6]{index=6}

---

## Documentation

📄 **Full project documentation:**  
[documentation.md](./documentation.md)

This file includes configuration steps, troubleshooting notes, flow log examples, and analysis performed during the project.

---

## Credits

Built as part of the **NextWork** AWS networking learning series.
