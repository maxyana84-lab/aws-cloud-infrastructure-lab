# AWS Cloud Infrastructure & High Availability Architecture

A hands-on DevOps project demonstrating the deployment of a scalable, fault-tolerant, and secure cloud infrastructure on Amazon Web Services (AWS).

---

## 🏗 Network & System Architecture

This project showcases a production-ready environment configured across multiple Availability Zones (AZs) to ensure high availability and redundancy.

### 📐 Key Infrastructure Components

* **VPC & Subnet Topology:** Custom Virtual Private Cloud (VPC) spanning multiple Availability Zones with isolated Public and Private Subnet tiers.
* **Traffic Routing (ALB):** Application Load Balancer (ALB) acting as the single point of entry to distribute incoming HTTP/HTTPS traffic across EC2 compute instances.
* **Shared Enterprise Storage:** Amazon Elastic File System (EFS) mounted to EC2 instances for persistent, concurrent shared filesystem storage across zones.
* **Network Security Layer:** Fine-grained AWS Security Groups enforcing strict principle-of-least-privilege rules for inbound/outbound traffic (Port 80/443 for ALB, NFS Port 2049 for EFS).

---

## 🛠 Tech Stack & Tools

* **Cloud Provider:** Amazon Web Services (AWS)
* **Compute & Load Balancing:** EC2 (RHEL/Ubuntu), Application Load Balancer (ALB), Target Groups
* **Storage & Networking:** Amazon EFS, VPC, Internet Gateway, Subnets, Route Tables
* **Security & Access Management:** AWS IAM, Security Groups, SSH Key Pairs

---

## ⚙️ Architecture Workflow & Execution Steps

1. **VPC & Subnet Setup:** Configured custom IP address ranges (CIDR blocks) across public and private availability zones.
2. **Security Groups Configuration:**
   - `ALB-SG`: Permits inbound HTTP (80) / HTTPS (443) from `0.0.0.0/0`.
   - `Instance-SG`: Accepts HTTP traffic *only* from `ALB-SG`.
   - `EFS-SG`: Accepts NFS traffic (Port 2049) *only* from `Instance-SG`.
3. **Compute & Storage Provisioning:**
   - Provisioned EC2 instances inside target subnets.
   - Attached shared EFS volumes via `nfs4` mount targets.
4. **Load Balancer Integration:** Attached instances to an ALB Target Group with active Health Checks enabled.

---

## 📌 Verification & Testing

- Verified HTTP responses via Load Balancer DNS Endpoint.
- Tested path-based routing and automatic instance target health status.
- Validated concurrent write/read access to shared EFS mount points across instances.
