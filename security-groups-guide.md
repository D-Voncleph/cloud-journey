# Security Groups: The Stateful Virtual Firewall 

This document explains the fundamental concept of AWS Security Groups (SGs), how they differ from other firewalls, and details the configuration used to secure the `MyFinanceTracker-Web-Server-1` instance.

## 1. Core Concepts and Statefulness

A Security Group acts as a **virtual firewall** for an individual resource, such as an EC2 instance.

* **Instance-Level:** The Security Group sits around the instance itself, not the subnet, filtering traffic just before it reaches the server.
* **Stateful:** This is the most critical feature. The SG **remembers the state of a connection**. If you allow traffic **out** (egress), the corresponding response traffic is automatically allowed **in** (ingress). This simplifies configuration significantly, as you only need to define rules for the traffic that initiates the connection.
* **Principle of Least Privilege:** SGs enforce this by blocking all inbound traffic by default. You must explicitly open the ports and IP addresses needed, and nothing else.

## 2. Configuration for `FinTech-Web-SG`

The `FinTech-Web-SG` was configured to enable a two-tier security model: allowing administrative access only to the owner, and web access to everyone.

| Rule Type | Protocol | Port | Source (IP/CIDR) | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **Inbound** (Admin Access) | **TCP** | **22 (SSH)** | **[Your Current Public IP]/32** | Allows secure terminal access only from my personal computer. |
| **Inbound** (Public Access) | **TCP** | **80 (HTTP)** | **0.0.0.0/0** | Allows anyone on the internet to view the web server (Nginx). |
| **Outbound** | ALL | ALL | 0.0.0.0/0 | Allows the server to make requests to the internet (e.g., download updates, fetch data). |

---