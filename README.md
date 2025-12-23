# VPC Monitoring with Flow Logs

**Project Link:** https://learn.nextwork.org/projects/aws-networks-monitoring  
**Author:** Shane Brown  

---

## Overview

This project focuses on monitoring network traffic inside Amazon Virtual Private Clouds (VPCs) using VPC Flow Logs. The goal is to gain visibility into how traffic flows between resources, how routing and peering affect connectivity, and how security rules allow or block traffic.

This project adds monitoring and observability to previously built VPC architectures.

---

## What I built

I configured network monitoring for a multi-VPC environment and analyzed traffic using AWS-native tools. This included:

- Creating multiple VPCs with non-overlapping CIDR blocks  
- Launching EC2 instances to generate network traffic  
- Enabling VPC Flow Logs  
- Sending flow logs to Amazon CloudWatch  
- Creating IAM roles and policies for log delivery  
- Testing connectivity and validating captured traffic  

This setup reflects how cloud teams monitor and troubleshoot network behavior in production.

---

## Key concepts learned

- What VPC Flow Logs capture and what they do not  
- How accepted and rejected traffic is recorded  
- How IAM roles and trust policies enable logging services  
- How CloudWatch log groups organize network data  
- How routing and VPC peering affect private traffic  
- Why monitoring is critical for security and troubleshooting  

---

## Monitoring network traffic

VPC Flow Logs capture metadata about traffic flowing through VPC resources, including:

- Source and destination IP addresses  
- Protocol and port information  
- Packet and byte counts  
- Accept or reject status  

These logs provide clear insight into how traffic behaves inside cloud networks without inspecting payload data.

---

## Testing and troubleshooting

I generated traffic between EC2 instances using `ping` and observed the results in VPC Flow Logs.

- Failed pings highlighted routing or peering misconfigurations  
- Successful pings confirmed private connectivity  
- Flow logs verified which traffic was allowed or denied  

This reinforced how monitoring tools support faster and more accurate troubleshooting.

---

## Analyzing flow logs

I used CloudWatch Logs Insights to query flow log data and identify traffic patterns, such as top source and destination IPs by data transfer.

Log analysis helps detect unusual activity, confirm expected behavior, and support incident investigation.

---

## Why this project matters

Monitoring is a critical layer of cloud networking and security. Without visibility, routing errors and security misconfigurations are difficult to detect.

This project demonstrates how AWS provides built-in tools to observe, analyze, and validate network traffic in a scalable and structured way.

---

## Documentation

📄 **Full project documentation:**  
[documentation.md](./documentation.md)

This file contains configuration steps, test results, flow log examples, and analysis from completing the project.

---

## Credits

Built as part of the **NextWork** AWS networking learning series.
