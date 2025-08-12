# AWS Cloud Database Modernization: IaaS to PaaS Migration

This project demonstrates how to migrate a MySQL database from an **EC2 instance (IaaS)** to **Amazon RDS (PaaS)** using `mysqldump` and restore.

---

## **Architecture**
![Architecture Diagram](images/architecture_diagram.png)

---

## **1️⃣ Create Database on EC2 (IaaS)**

```bash
# Connect to EC2 instance via SSH
ssh -i mykey.pem ec2-user@<EC2_PUBLIC_IP>

# Install MySQL server
sudo yum update -y
sudo yum install -y mariadb-server

# Start MySQL service
sudo systemctl start mariadb
sudo systemctl enable mariadb

# Login to MySQL
mysql -u root -p
-- Create database
CREATE DATABASE fct;

-- Use database
USE fct;

-- Create table
CREATE TABLE studentInfo (
    SR_no INT PRIMARY KEY,
    NAME VARCHAR(50),
    Crouse VARCHAR(50)
);

-- Insert sample records
INSERT INTO studentInfo VALUES (101, 'tejal', 'aws');
INSERT INTO studentInfo VALUES (102, 'ishwar', 'java');
INSERT INTO studentInfo VALUES (103, 'isha', 'aws');

-- Verify data
SELECT * FROM studentInfo;
# Exit MySQL
exit;

# Exit EC2 SSH
exit

---

## 📦 Step 4: Backup Database from EC2 (IaaS)


