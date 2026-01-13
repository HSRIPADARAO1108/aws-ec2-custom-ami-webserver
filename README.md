# aws-ec2-custom-ami-webserver

# AWS Infrastructure: Immutable Web Server using Custom AMIs

## 1. Project Overview
This project demonstrates the transition from **Manual Server Configuration** to **Automated Infrastructure** using the "Golden Image" strategy. By utilizing Amazon Machine Images (AMI), I eliminated the need to manually configure web servers, ensuring 100% consistency and rapid deployment.



---

## 2. What is an AMI? (The Solution)
An **Amazon Machine Image (AMI)** is a read-only boot disk image used to create a virtual machine in EC2.
* **The Problem:** Setting up a server manually (installing OS updates, web servers, and code) takes 10-20 minutes and is prone to human error.
* **The Solution:** I configured a "Golden Instance" once, "froze" it into an AMI, and used that AMI to launch pre-configured clones instantly.

---

## 3. Comparison: Manual vs. AMI Deployment
| Factor | Manual Configuration | AMI (Golden Image) |
| :--- | :--- | :--- |
| **Setup Speed** | Slow (15+ mins) | Instant (< 1 min) |
| **Reliability** | Low (Risk of "Configuration Drift") | High (Bit-for-bit identical) |
| **Scalability** | Difficult to repeat | Perfect for Auto Scaling Groups |

---

## 4. Technical Implementation

### Step 1: Baseline Build
* Launched a base **Ubuntu 24.04 LTS** instance (`t2.micro`).
* Connected via SSH and performed system hardening:
  ```bash
  sudo apt update && sudo apt upgrade -y
  sudo apt install apache2 -y
  sudo systemctl enable apache2
