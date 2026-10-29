# Cloud, DevOps & Data Analytics Portfolio

A collection of hands-on projects covering AWS Cloud, DevOps automation, database management, serverless applications, monitoring, data visualization, and AI tools.

This repository documents project objectives, implementation steps, configurations, screenshots, validation results, troubleshooting, and key technical learnings.

## About This Repository

The goal of this portfolio is to demonstrate practical skills in cloud infrastructure, automation, database operations, deployment pipelines, observability, data analytics, and AI-assisted workflows.

Each project will include step-by-step documentation and evidence of implementation as the work progresses.

## Technical Areas

- **Cloud Computing:** AWS infrastructure and managed services
- **Database Services:** Amazon Aurora, database backup strategies
- **Serverless Computing:** Serverless APIs and AWS Lambda
- **Security & Encryption:** AWS Key Management Service (KMS)
- **Storage:** Amazon Elastic File System (EFS)
- **DevOps & Automation:** AWS Elastic Beanstalk, deployment pipelines, Ansible
- **Monitoring & Observability:** Grafana dashboards
- **Data Analytics & Visualization:** Power BI, Tableau
- **AI Tools:** Gemini and related AI workflows

## Project Roadmap

### 1. AWS Cloud Projects

| # | Project | Description | Status |
|---:|---|---|---|
| 1 | [Create an Auto Scaling Group](./aws/01-auto-scaling-group/) | Create an EC2 Launch Template and Auto Scaling Group, configure capacity, and test automatic instance replacement. | Done |
| 2 | [Deploy and Test an Amazon RDS MySQL Database](./Deploy%20and%20Test%20an%20Amazon%20RDS%20MySQL%20Database/) | Provision an Amazon RDS for MySQL instance, configure connectivity and security, validate SQL operations, and clean up resources. | Done |
| 3 | [Create a Serverless API](./aws/03-serverless-api/) | Build a serverless API using AWS Lambda and Amazon API Gateway. | Planned |
| 4 | [Create a KMS Customer Managed Key and Encrypt an Object](./aws/04-kms-encryption/) | Create a customer managed key in AWS KMS and use it to encrypt an object in Amazon S3. | Planned |
| 5 | [Create an EFS Shared File System](./aws/05-efs-shared-file-system/) | Configure Amazon EFS and explore shared file access from EC2 instances. | Planned |
| 6 | [AWS Deployment Pipeline Using Elastic Beanstalk](./aws/06-elastic-beanstalk-pipeline/) | Deploy an application using AWS Elastic Beanstalk and build an automated deployment workflow. | Planned |

### 2. DevOps & Configuration Management

| # | Project | Description | Status |
|---:|---|---|---|
| 7 | [Configure a Linux Server Using Ansible](./devops/07-ansible-linux-configuration/) | Write an Ansible playbook to automate Linux server configuration and package installation. | Planned |

### 3. Monitoring & Data Analytics

| # | Project | Description | Status |
|---:|---|---|---|
| 9 | [Create a Grafana Dashboard](./monitoring/09-grafana-dashboard/) | Build a Grafana dashboard to visualize metrics and monitor system performance. | Planned |
| 10 | [Create a Power BI Dashboard](./data-analytics/10-power-bi-dashboard/) | Transform data into an interactive Power BI dashboard with meaningful visualizations. | Planned |
| 11 | [Create a Tableau Dashboard](./data-analytics/11-tableau-dashboard/) | Build an interactive Tableau dashboard to explore data and communicate insights. | Planned |

### 4. Database Backup & AI Tools

| # | Project | Description | Status |
|---:|---|---|---|
| 8 | [Automated Database Backups Using Cloudflare](./database/08-cloudflare-db-backups/) | Investigate and implement an appropriate Cloudflare-based workflow for automating database backups. | Planned |
| 12 | [Configure Gemini Spark](./ai-tools/12-gemini-spark/) | Explore the intended Gemini Spark tool or service, configure it, and document its capabilities and use cases. | Planned |

> **Note:** Project 8 and Project 12 need their exact tools or architecture confirmed before implementation. Cloudflare is not a general-purpose managed database backup service, and "Gemini Spark" may refer to a specific product or workflow.

## Repository Structure

```text
cloud-devops-portfolio/
├── README.md
├── aws/
│   ├── 01-auto-scaling-group/
│   ├── 02-aurora-rds-database/
│   ├── 03-serverless-api/
│   ├── 04-kms-encryption/
│   ├── 05-efs-shared-file-system/
│   └── 06-elastic-beanstalk-pipeline/
├── devops/
│   └── 07-ansible-linux-configuration/
├── database/
│   └── 08-cloudflare-db-backups/
├── monitoring/
│   └── 09-grafana-dashboard/
├── data-analytics/
│   ├── 10-power-bi-dashboard/
│   └── 11-tableau-dashboard/
└── ai-tools/
    └── 12-gemini-spark/
```

## What Each Project Will Include

Where applicable, each project will contain:

- **Overview:** Problem statement and project objectives.
- **Architecture:** Services, components, and their relationships.
- **Prerequisites:** Required tools, permissions, and configuration.
- **Implementation:** Step-by-step instructions.
- **Configuration:** Relevant scripts, templates, and settings.
- **Validation:** Tests and evidence confirming the outcome.
- **Screenshots:** Console views, dashboards, and deployment results.
- **Troubleshooting:** Issues encountered and their resolutions.
- **Cleanup:** Instructions for removing resources and avoiding unnecessary charges.
- **Key Learnings:** Concepts and practical skills demonstrated.

## Learning Objectives

- Provision and manage AWS cloud infrastructure.
- Configure scalable applications, managed databases, and shared storage.
- Implement encryption and access controls.
- Build serverless applications and deployment pipelines.
- Automate Linux configuration with Ansible.
- Explore database backup automation.
- Create monitoring dashboards and business intelligence reports.
- Evaluate AI tools through practical configuration and documentation.

## Progress Tracking

Projects will be marked as completed only after implementation and validation. Planned work will remain clearly identified until the relevant steps and results have been documented.

## Disclaimer

This repository is intended for learning, experimentation, and portfolio development. AWS resources may incur charges. Review service pricing, secure credentials, and clean up unused resources after testing.

## Connect

For professional opportunities and technical discussions, connect through GitHub or LinkedIn.
