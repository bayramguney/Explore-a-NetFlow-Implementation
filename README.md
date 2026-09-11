# Explore-a-NetFlow-Implementation
# NetFlow Flow Records Lab

## Overview
This lab demonstrates how Cisco NetFlow monitors and records network traffic. Using Packet Tracer, ICMP, HTTP, and DNS traffic were generated and analyzed with the NetFlow Collector to understand how flows are created, tracked, and displayed based on source/destination addresses, protocols, ports, and interfaces.

## Objectives
- Observe one-way NetFlow flow records.
- Understand how NetFlow identifies unique network flows.
- Analyze HTTP request and response traffic.
- Observe DNS traffic when accessing a website by URL.
- Compare request and response flow records.

## Technologies Used
- Cisco Packet Tracer
- Cisco NetFlow
- ICMP (Ping)
- HTTP
- DNS
- TCP/UDP

## Key Observations

### Part 1 – One-Way Flow Records
- A ping from **PC-1** to the default gateway created a NetFlow record.
- When **PC-2** pinged the gateway, a **new flow** appeared because the source IP address was different.
- Additional pings from **PC-1** updated the existing flow by increasing the packet and byte counters.
- Pings from **PC-3** and **PC-4** created additional flow records, resulting in multiple segments in the collector's pie chart.

## HTTP Session Analysis
Accessing the web server by IP address generated at least two flows:

| Flow | Description |
|------|-------------|
| HTTP Request | PC-1 → Web Server (TCP Destination Port 80) |
| HTTP Response | Web Server → PC-1 (TCP Source Port 80) |

The HTTP request used a dynamically assigned client (ephemeral) source port, while the response returned to that same port.

Selecting another webpage (Copyrights) reused the existing TCP session, so the existing NetFlow record was updated instead of creating a completely new connection.

## DNS and HTTP Traffic
When accessing the server using **www.example.com**, additional DNS traffic appeared before the HTTP connection.

Typical flows included:
- DNS Request (UDP)
- DNS Response (UDP)
- HTTP Request (TCP)
- HTTP Response (TCP)

ARP traffic may also appear if address resolution is required.

## IP Protocol Values

| Protocol Number | Protocol | Purpose |
|-----------------|----------|---------|
| 1 | ICMP | Ping traffic |
| 6 | TCP | HTTP communication |
| 17 | UDP | DNS queries and responses |

## What I Learned
- NetFlow identifies a flow using attributes such as source/destination IP addresses, protocol, and ports.
- Traffic from different hosts creates separate flow records.
- Repeated traffic within the same session updates an existing flow instead of creating a new one.
- HTTP communication generates separate request and response flows.
- Using a URL introduces additional DNS flows before the HTTP session begins.
- NetFlow provides valuable visibility into network communication patterns for monitoring, troubleshooting, and security analysis.

## Skills Demonstrated
- Cisco NetFlow Monitoring
- Packet Analysis
- Flow Record Interpretation
- TCP/IP Networking
- ICMP, TCP, and UDP Traffic Analysis
- HTTP and DNS Traffic Inspection
- Network Monitoring and Troubleshooting
- Cisco Packet Tracer
