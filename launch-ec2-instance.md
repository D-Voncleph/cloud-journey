# Step-by-Step Guide: Launching and Connecting to an EC2 Instance

This guide provides a detailed walkthrough of the process of creating and connecting to a virtual server (EC2 instance) on AWS. It covers best practices for instance configuration and secure access.

## 1. Create and Secure Your Key Pair 🔑

The first step is to generate an SSH key pair on your local machine, which is a more secure way to authenticate than using a password.

1.  Open your terminal on your local machine.
2.  Run the following command to generate a new key pair:
    ```bash
    ssh-keygen -t rsa -b 4096 -f ~/.ssh/my-ec2-key
    ```
3.  When prompted for a passphrase, you can press **Enter** twice to leave it empty for now. This command creates a private key (`my-ec2-key`) and a public key (`my-ec2-key.pub`).

4.  Before launching your instance, go to the **EC2 dashboard** in the AWS console.
5.  On the left-hand menu, under "Network & Security," click **"Key pairs."**
6.  Click the **"Import key pair"** button. Give it the same name you used (`my-ec2-key`), and upload the **`my-ec2-key.pub`** file from your `~/.ssh/` directory.

## 2. Launch the EC2 Instance 🚀

Now, you will use the AWS Management Console to launch your virtual server.

1.  Go back to the EC2 dashboard and click the **"Launch instance"** button.

2.  **Name:** Give your instance a professional name (e.g., `MyFinanceTracker-Web-Server-1`).

3.  **AMI (Application and OS Images):** Select a stable, long-term support version, such as **Ubuntu 22.04 LTS**.

4.  **Instance type:** Choose **`t3.micro`**, which is a Free Tier eligible instance type.

5.  **Key pair:** Select **`my-ec2-key`** from the dropdown menu.

6.  **Network settings:** Create a new security group that allows traffic on **SSH (Port 22)** and **HTTP (Port 80)** from "Anywhere."

7.  Click the **"Launch instance"** button.

## 3. Connect to the Instance via SSH 💻

Once your instance is running, you can connect to it from your local terminal.

1.  Go back to the EC2 dashboard and find the **Public IPv4 address** for your new instance.

2.  In your local terminal, set the correct permissions on your private key:
    ```bash
    chmod 400 ~/.ssh/my-ec2-key
    ```

3.  Connect to your instance using the default `ubuntu` username and the public IP address:
    ```bash
    ssh -i ~/.ssh/my-ec2-key ubuntu@<your-instance-public-ip>
    ```

---

### Connect with me

[LinkedIn](https://www.linkedin.com/in/voncleph) | [GitHub](https://github.com/D-Voncleph)