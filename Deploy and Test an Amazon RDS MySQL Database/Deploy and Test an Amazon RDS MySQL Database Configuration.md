# Deploy and Test an Amazon RDS MySQL Database

## Cloud Service Provider

- Amazon Web Services (AWS)

## Difficulty

- Level 200 — Intermediate

## Project Overview

Provisioned an Amazon RDS for MySQL database in AWS, configured network connectivity and security settings, connected remotely using MySQL Workbench, and validated database operations by creating a table, inserting records, and executing SQL queries. Deleted the database after verification to minimize ongoing infrastructure costs.

**Note:** The original exercise specified Amazon Aurora MySQL. Aurora MySQL was unavailable under the account's plan restrictions, so the implementation used standard Amazon RDS for MySQL instead.

## Objectives

The project covered the following tasks:

- Configure an RDS MySQL database in the AWS Region's default VPC.
- Select the MySQL Community engine and MySQL 8.4.11.
- Configure a development database using the available Free Tier template.
- Deploy a Single-AZ DB instance using the `db.t4g.micro` instance class.
- Configure 20 GiB of general-purpose SSD storage.
- Create and attach the `aurora-mysql-test-sg` security group.
- Configure public accessibility and MySQL connectivity on TCP port `3306`.
- Set a custom master username and password.
- Connect remotely to the database using MySQL Workbench.
- Create a database and verification table.
- Insert test data and validate the results using SQL queries.
- Delete the RDS instance after successful verification.

## Implementation

### 1. Database Provisioning

Created an Amazon RDS for MySQL instance in the Asia Pacific (Hyderabad) Region (`ap-south-2`).

**Configuration:**

- Engine: MySQL Community
- Engine version: MySQL 8.4.11
- DB instance identifier: `dbs03-mysql-test`
- Instance class: `db.t4g.micro`
- Storage: 20 GiB General Purpose SSD
- Deployment: Single-AZ
- VPC: Default VPC
- Database port: `3306`

### 2. Network Connectivity and Security

Configured the database to support remote connections from a local MySQL client.

- Selected the default VPC and default DB subnet group.
- Enabled public accessibility for the development exercise.
- Attached the `aurora-mysql-test-sg` security group.
- Used an inbound MySQL rule on TCP port `3306`.

Public database access is appropriate only for controlled testing with suitable restrictions. Production deployments should generally keep databases private or restrict access to trusted sources.

### 3. Remote Database Connection

Connected to the RDS instance from a local computer using MySQL Workbench.

Verified connectivity by executing:

```sql
SELECT VERSION();
```

The query returned MySQL version `8.4.11`, confirming that the remote database connection was functional.

### 4. Database and Table Creation

Created a test database and verification table using SQL.

```sql
CREATE DATABASE IF NOT EXISTS projectdb;

USE projectdb;

CREATE TABLE IF NOT EXISTS project_verification (
    id INT AUTO_INCREMENT PRIMARY KEY,
    project_name VARCHAR(100) NOT NULL,
    cloud_provider VARCHAR(50) NOT NULL,
    database_engine VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 5. Data Insertion and Verification

Inserted a test record into the table.

```sql
INSERT INTO project_verification
    (project_name, cloud_provider, database_engine)
VALUES
    ('DBS03-AWS200', 'AWS', 'RDS MySQL');
```

Verified the inserted record using:

```sql
SELECT * FROM project_verification;
```

**Result:** The query returned the expected record, confirming that table creation, data insertion, and data retrieval worked successfully.

## Technical Concepts Demonstrated

### Amazon RDS

Amazon Relational Database Service is a managed database service that simplifies database provisioning, administration, backups, monitoring, and infrastructure management.

### Instance-Based vs. Serverless Databases

Provisioned RDS instances use a selected DB instance class with defined compute and memory resources. Serverless database offerings adjust compute capacity based on workload and configuration.

This project used a provisioned RDS MySQL instance rather than Aurora Serverless.

### VPC and Security Groups

A VPC provides the network environment for AWS resources. Security groups act as stateful virtual firewalls that control permitted inbound and outbound traffic.

For this implementation, MySQL connectivity used TCP port `3306`.

### Public Accessibility

Public accessibility allowed the local MySQL Workbench client to connect without deploying a client application on an EC2 instance. This configuration requires appropriate routing, security-group rules, and database authentication.

For production, private connectivity and least-privilege network rules are preferred.

### Database Encryption

Amazon RDS supports encryption at rest using AWS Key Management Service (AWS KMS). Encryption in transit can also be configured to protect client-to-database connections.

### SQL Validation

The project demonstrated common SQL operations:

- `CREATE DATABASE` — create a database.
- `CREATE TABLE` — define a table and its columns.
- `INSERT` — add a record.
- `SELECT` — retrieve and validate data.
- `DESCRIBE` — inspect the table structure.

## Results

- Successfully provisioned an Amazon RDS for MySQL database.
- Established a remote connection using MySQL Workbench.
- Verified the database engine version.
- Created a database and test table.
- Inserted and retrieved a test record successfully.
- Deleted the RDS instance after testing to avoid unnecessary ongoing compute charges.

## Cleanup and Cost Management

The RDS instance was deleted after the database operations were verified. Final snapshot creation and automated backup retention were disabled during deletion because the test data was no longer required.

The associated security group and any remaining backup resources should be checked separately to ensure that unused resources do not remain.

## Key Learnings

- Provisioning and configuring managed relational databases on AWS.
- Understanding RDS instance classes, storage, VPCs, and security groups.
- Establishing remote database connectivity from a local SQL client.
- Creating schemas and tables and validating data through SQL.
- Applying basic network security principles to publicly accessible databases.
- Cleaning up cloud resources after completing a development exercise.

## References

- [Amazon RDS Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [Creating an Amazon RDS DB Instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateDBInstance.html)
- [Amazon RDS Pricing](https://aws.amazon.com/rds/pricing/)
- [MySQL Workbench Downloads](https://dev.mysql.com/downloads/workbench/)

## Project Evidence

Recommended screenshots:

1. RDS database overview and instance configuration.
2. Connectivity and security configuration.
3. MySQL Workbench connection and engine version.
4. SQL table creation, insertion, and successful query results.

**Project status:** Core database provisioning, connectivity, SQL validation, and RDS instance deletion completed.

**Scope note:** This implementation demonstrates Amazon RDS for MySQL. Aurora-specific features, including Aurora storage architecture, reader endpoints, Aurora Replicas, and Aurora Global Database, were not deployed or tested in this project.
