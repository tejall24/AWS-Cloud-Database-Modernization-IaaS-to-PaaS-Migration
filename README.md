# AWS Cloud Database Modernization: IaaS to PaaS Migration


---

## 1️⃣ Step 1: Create Database on EC2 (IaaS)
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
---

## 2️⃣ Step 2: Insert Sample Data into EC2 Database
# Login to MySQL on EC2
mysql -u root -p
# (enter the MySQL root password when prompted)

-- create database and table
CREATE DATABASE fct;
USE fct;

CREATE TABLE studentInfo (
  SR_no INT PRIMARY KEY,
  NAME VARCHAR(50),
  Crouse VARCHAR(50)
);

-- insert sample data
INSERT INTO studentInfo VALUES (101, 'tejal', 'aws');
INSERT INTO studentInfo VALUES (102, 'ishwar', 'java');
INSERT INTO studentInfo VALUES (103, 'isha', 'aws');

-- verify
SELECT * FROM studentInfo;

-- exit MySQL
EXIT;

---

## 3️⃣ Step 3: Verify EC2 Database Data
# still on EC2 (or re-SSH if you exited)
mysql -u root -p -e "USE fct; SELECT * FROM studentInfo;"
# This prints the table contents directly in shell.


---

## 📦 Step 4: Backup Database from EC2 (IaaS)
# on EC2 terminal
mysqldump -u root -p fct > fct_backup.sql
# enter mysql root password when prompted

# verify file
ls -lh fct_backup.sql

---

## 📤 Step 5: Transfer Backup File to Local or RDS Host
# From local machine, copy from EC2 to local (replace values)
scp -i mykey.pem ec2-user@<EC2_PUBLIC_IP>:~/fct_backup.sql .

# If compressed:
scp -i mykey.pem ec2-user@<EC2_PUBLIC_IP>:~/fct_backup.sql.gz .

---

## ☁️ Step 6: Restore Backup to Amazon RDS (PaaS)
# Restore from local machine to RDS
mysql -h <RDS_ENDPOINT> -u admin -p rdsdb < fct_backup.sql
# when prompted, enter RDS master password

---

## 🔍 Step 7: Verify Data on RDS Database
# connect to RDS and inspect
mysql -h <RDS_ENDPOINT> -u admin -p

# inside mysql prompt:
SHOW DATABASES;
USE rdsdb;
SHOW TABLES;
SELECT * FROM studentInfo;
EXIT;

---

## 🏗 Step 8: AWS Architecture Diagram

---
