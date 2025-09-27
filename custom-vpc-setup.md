# Custom VPC and Public Subnet Configuration Guide 🌐

This guide documents the manual, step-by-step process of building a custom VPC with a single public subnet. This setup is the network backbone for our FinTech application.

## 1. VPC and Subnet Creation

The first step is defining the boundaries of our private network and segmenting it.

| Component | Name | CIDR Range (IP Address Range) | Purpose |
| :--- | :--- | :--- | :--- |
| **VPC** | `FinTech-VPC` | `10.10.0.0/16` | **The entire isolated network (65,536 addresses).** |
| **Subnet** | `FinTech-Public-Subnet-A` | `10.10.1.0/24` | **A small segment within the VPC (256 addresses).** |

### Manual Creation Steps:

1.  **Create VPC:** In the VPC Console, select **"Create VPC"** and choose **"VPC only."** Use the CIDR block `10.10.0.0/16` and the name `FinTech-VPC`.
2.  **Create Subnet:** Navigate to "Subnets" and click **"Create subnet."** Select the `FinTech-VPC` and assign the CIDR block `10.10.1.0/24` with the name `FinTech-Public-Subnet-A`.

## 2. Enabling Internet Access (The Routing Logic)

To make this subnet public, two manual components must be linked: the **Internet Gateway** and the **Route Table**.

### The Role of the Route Table 🚦

The **Route Table** is the "traffic cop" of the VPC. It contains a set of rules (routes) that tell network traffic where to go. The custom Route Table for a public subnet must explicitly have a rule that directs traffic outside the VPC to the Internet Gateway.

### Configuration Steps:

1.  **Create Internet Gateway (IGW):** Create a new IGW (e.g., `FinTech-IGW`) and use **Actions** to **Attach** it to the `FinTech-VPC`.
2.  **Create Custom Route Table:** Create a new Route Table (`FinTech-Public-RT`) and associate it with the `FinTech-VPC`.
3.  **Associate Subnet:** Associate the `FinTech-Public-RT` with the `FinTech-Public-Subnet-A`.
4.  **Add the Public Route:** Under the "Routes" tab, add the following rule:
    * **Destination:** `0.0.0.0/0` (Represents "all traffic on the public internet").
    * **Target:** Select the **Internet Gateway** (`FinTech-IGW`).
5.  **Final Step:** Enable "Auto-assign Public IPv4 address" on the `FinTech-Public-Subnet-A` settings page so that instances launched there automatically receive a public IP.