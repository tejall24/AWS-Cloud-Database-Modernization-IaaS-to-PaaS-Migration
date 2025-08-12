# AWS Cloud Database Modernization: IaaS to PaaS Migration

## 📖 Introduction
This project demonstrates the migration of a MySQL database from an EC2 instance (IaaS) to an Amazon RDS instance (PaaS).  
It covers:
- Creating a database (`fct`) and table (`studentInfo`) on EC2
- Inserting sample data
- Backing up the EC2 database
- Restoring the backup into an RDS database (`rdsdb`)
- Verifying the data after migration
- Presenting the AWS architecture and final output screenshots

---

## 🏗 Architecture Diagram
![Architecture Diagram](images/architecture_diagram.png)

---

## 1️⃣ Step 1: Create Database on EC2 (IaaS)
```bash
ssh -i mykey.pem ec2-user@<EC2_PUBLIC_IP>
sudo yum update -y
sudo yum install -y mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation
exit
````

##2️⃣ Step 2: Insert Sample Data into EC2 Database
bash
Copy
Edit
mysql -u root -p
CREATE DATABASE fct;
USE fct;
CREATE TABLE studentInfo (
  SR_no INT PRIMARY KEY,
  NAME VARCHAR(50),
  Crouse VARCHAR(50)
);
INSERT INTO studentInfo VALUES (101, 'tejal', 'aws');
INSERT INTO studentInfo VALUES (102, 'ishwar', 'java');
INSERT INTO studentInfo VALUES (103, 'isha', 'aws');
SELECT * FROM studentInfo;
EC2 Database Output:
exit
````
📦 Step 3: Backup Database from EC2 (IaaS)
bash
Copy
Edit
mysqldump -u root -p fct > fct_backup.sql
📤 Step 4: Transfer Backup File
If copying from EC2 to your local machine:

bash
Copy
Edit
scp -i mykey.pem ec2-user@<EC2_PUBLIC_IP>:~/fct_backup.sql .
If copying from local to another EC2/RDS environment:

bash
Copy
Edit
scp -i mykey.pem fct_backup.sql ec2-user@<DESTINATION_IP>:/home/ec2-user/
☁️ Step 5: Restore Backup to Amazon RDS (PaaS)
bash
Copy
Edit
mysql -h <RDS_ENDPOINT> -u admin -p -e "CREATE DATABASE IF NOT EXISTS rdsdb;"
mysql -h <RDS_ENDPOINT> -u admin -p rdsdb < fct_backup.sql
🔍 Step 6: Verify Data on RDS Database
bash
Copy
Edit
mysql -h <RDS_ENDPOINT> -u admin -p
USE rdsdb;
SELECT * FROM studentInfo;
RDS Database Output:

📊 AWS RDS Instance Screenshot

✅ Conclusion
This workflow successfully migrates a MySQL database from EC2 (IaaS) to RDS (PaaS) using AWS services.
It demonstrates:

Database provisioning on EC2

Data backup and restoration

Cloud database management in RDS

Verification of successful migration
