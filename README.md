# AWS Cloud Database Modernization: IaaS to PaaS Migration
# SSH into EC2 (replace values)
ssh -i mykey.pem ec2-user@<EC2_PUBLIC_IP>

# Update packages & install MariaDB/MySQL
sudo yum update -y
sudo yum install -y mariadb-server    # Or use mysql-server on ubuntu: sudo apt install -y mysql-server

# Start and enable service
sudo systemctl start mariadb
sudo systemctl enable mariadb

# Secure installation (optional interactive)
sudo mysql_secure_installation

---

## 1️⃣ Step 1: Create Database on EC2 (IaaS)

---

## 2️⃣ Step 2: Insert Sample Data into EC2 Database

---

## 3️⃣ Step 3: Verify EC2 Database Data

---

## 📦 Step 4: Backup Database from EC2 (IaaS)

---

## 📤 Step 5: Transfer Backup File to Local or RDS Host

---

## ☁️ Step 6: Restore Backup to Amazon RDS (PaaS)

---

## 🔍 Step 7: Verify Data on RDS Database

---

## 🏗 Step 8: AWS Architecture Diagram

---
