---
title: AWS FedRAMP-Authorized Services Reference
---

# AWS FedRAMP-Authorized Services Reference

AWS maintains FedRAMP authorization across hundreds of services. Below are the services most commonly needed for federal workloads pursuing FedRAMP Moderate or High authorization.

**Note:** Authorization levels and details are subject to change. Always check [fedramp.gov/marketplace](https://marketplace.fedramp.gov) and the [AWS FedRAMP Compliance page](https://aws.amazon.com/compliance/fedramp/) for current certification status.

---

## Governance & Management

| AWS Service                     | FedRAMP Level | Primary Use in FedRAMP                    | Key Controls      |
| ------------------------------- | ------------- | ----------------------------------------- | ----------------- |
| **AWS Organizations**           | High          | Multi-account structure and governance    | AC-2, AC-3, SC-7  |
| **AWS Control Tower**           | High          | Account provisioning with guardrails      | CM-2, CM-6, CA-7  |
| **AWS Systems Manager**         | High          | Patch management and configuration        | CM-2, SI-2, SI-7  |
| **AWS CloudFormation**          | High          | Infrastructure as Code deployment         | CM-3, SA-3, SA-10 |
| **AWS Service Catalog**         | High          | Self-service provisioning with governance | AC-3, CM-2, SA-6  |
| **AWS Resource Access Manager** | High          | Share resources across accounts           | AC-2, SC-7        |

---

## Logging & Monitoring

| AWS Service             | FedRAMP Level | Primary Use in FedRAMP                   | Key Controls            |
| ----------------------- | ------------- | ---------------------------------------- | ----------------------- |
| **AWS CloudTrail**      | High          | Audit logging of API calls               | AU-2, AU-3, AU-9, AU-11 |
| **Amazon CloudWatch**   | High          | Metrics, logs, alarms, dashboards        | CA-7, SI-4, AU-2        |
| **AWS Config**          | High          | Configuration compliance monitoring      | CM-2, CA-7, CM-6        |
| **Amazon Security Hub** | High          | Centralized security findings            | CA-2, CA-7, RA-5        |
| **Amazon GuardDuty**    | High          | Threat detection (VPC, CloudTrail)       | IR-4, SI-4, IR-5        |
| **Amazon Macie**        | Moderate      | S3 data classification and PII detection | SI-4, SC-28, CA-7       |
| **AWS CloudWatch Logs** | High          | Centralized log aggregation              | AU-2, AU-3, AU-11       |

---

## Identity & Access Management

| AWS Service                                  | FedRAMP Level | Primary Use in FedRAMP             | Key Controls                 |
| -------------------------------------------- | ------------- | ---------------------------------- | ---------------------------- |
| **AWS Identity and Access Management (IAM)** | High          | User/role/policy management        | AC-2, AC-3, AC-6, IA-2, IA-5 |
| **AWS IAM Identity Center**                  | High          | Centralized identity and SSO       | AC-2, IA-2, IA-5             |
| **Amazon Cognito**                           | High          | User authentication and federation | IA-2, IA-2(1), IA-5          |
| **AWS Secrets Manager**                      | High          | Credential rotation and storage    | IA-5, IA-5(1), SC-12         |
| **AWS KMS**                                  | High          | Cryptographic key management       | SC-12, SC-12(1), SC-28       |
| **AWS Certificate Manager**                  | High          | TLS/SSL certificate provisioning   | SC-8, SC-13                  |

---

## Network & Boundary Protection

| AWS Service              | FedRAMP Level                           | Primary Use in FedRAMP              | Key Controls            |
| ------------------------ | --------------------------------------- | ----------------------------------- | ----------------------- |
| **Amazon VPC**           | High                                    | Virtual private cloud and isolation | SC-7, SC-7(3), AC-17    |
| **AWS Transit Gateway**  | High                                    | Multi-account network connectivity  | SC-7, SC-7(3)           |
| **AWS PrivateLink**      | High                                    | Private access to AWS services      | SC-7, SC-8, AC-17       |
| **AWS WAF**              | High                                    | Web application firewall            | SC-5, SC-7, SI-3, SI-10 |
| **AWS Shield**           | Standard (free), DDoS Protection (paid) | DDoS mitigation                     | SC-5                    |
| **AWS Network Firewall** | High                                    | Stateful firewall inspection        | SC-7, SI-3, SI-4        |
| **Amazon Route 53**      | High                                    | DNS service                         | SC-8, AC-3              |
| **VPC Flow Logs**        | High                                    | Network traffic logging             | AU-2, SI-4, AU-11       |

---

## Data Protection & Encryption

| AWS Service                     | FedRAMP Level | Primary Use in FedRAMP               | Key Controls                     |
| ------------------------------- | ------------- | ------------------------------------ | -------------------------------- |
| **AWS KMS**                     | High          | Key management service               | SC-12, SC-12(1), SC-28, SC-28(1) |
| **Amazon S3**                   | High          | Object storage (logs, data, backups) | SC-28, SC-28(1), AU-11           |
| **Amazon S3 Object Lock**       | High          | Immutable log storage (WORM)         | AU-9, AU-11, SC-28               |
| **AWS Database Encryption Key** | High          | EBS volume encryption                | SC-28, SC-28(1)                  |
| **AWS CloudHSM**                | High          | Dedicated hardware security module   | SC-12, SC-12(1), SC-13           |

---

## Compute & Containers

| AWS Service    | FedRAMP Level | Primary Use in FedRAMP            | Key Controls            |
| -------------- | ------------- | --------------------------------- | ----------------------- |
| **Amazon EC2** | High          | Virtual machines                  | CM-7, SI-3, SI-7        |
| **AWS Lambda** | High          | Serverless functions              | CM-7, SA-3, SA-10       |
| **Amazon ECS** | High          | Container orchestration (Fargate) | CM-7, SI-3, SI-7        |
| **Amazon EKS** | Moderate      | Kubernetes service                | CM-7, SI-3, SI-7        |
| **Amazon ECR** | High          | Container image registry          | SA-10, SI-3, SI-7, CM-7 |

---

## Database & Data

| AWS Service                        | FedRAMP Level | Primary Use in FedRAMP                | Key Controls                 |
| ---------------------------------- | ------------- | ------------------------------------- | ---------------------------- |
| **Amazon RDS**                     | High          | Managed relational database           | SI-10, SC-28, SC-28(1), AU-2 |
| **Amazon Aurora**                  | High          | High-availability relational database | SC-28, SC-28(1), CP-2        |
| **Amazon DynamoDB**                | High          | NoSQL database                        | SC-28, SC-28(1), AU-2        |
| **Amazon OpenSearch Service**      | Moderate      | Search and log analytics              | CA-7, SI-4                   |
| **AWS Database Migration Service** | High          | Database migration tool               | SA-3, SI-7                   |
| **Amazon ElastiCache**             | High          | In-memory caching (encrypted)         | SC-28, SC-28(1)              |

---

## Application Integration & AI/ML

| AWS Service            | FedRAMP Level | Primary Use in FedRAMP        | Key Controls       |
| ---------------------- | ------------- | ----------------------------- | ------------------ |
| **AWS API Gateway**    | High          | RESTful and WebSocket APIs    | AC-17, SC-8, SI-10 |
| **Amazon SQS**         | High          | Message queue service         | SC-8, SC-12        |
| **Amazon SNS**         | High          | Publish/subscribe messaging   | SC-8, CA-7         |
| **AWS Step Functions** | High          | Orchestration and workflows   | CA-7, CM-7         |
| **Amazon Bedrock**     | Moderate      | Managed generative AI service | SI-4, CA-2, SA-11  |
| **Amazon SageMaker**   | Moderate      | Machine learning platform     | SA-3, SI-4, CA-2   |

---

## Security & Compliance

| AWS Service                 | FedRAMP Level | Primary Use in FedRAMP       | Key Controls     |
| --------------------------- | ------------- | ---------------------------- | ---------------- |
| **AWS WAF**                 | High          | Web application firewall     | SC-5, SC-7, SI-3 |
| **AWS Shield**              | High          | DDoS protection              | SC-5             |
| **Amazon Inspector**        | High          | Vulnerability assessments    | RA-5, SI-2, SI-4 |
| **AWS Secrets Manager**     | High          | Secrets storage and rotation | IA-5, SC-12      |
| **AWS KMS**                 | High          | Encryption key management    | SC-12, SC-28     |
| **AWS Certificate Manager** | High          | TLS certificate provisioning | SC-8, SC-13      |
| **AWS Artifact**            | High          | Compliance documentation     | CA-2, CA-8       |

---

## Developer Tools & CI/CD

| AWS Service            | FedRAMP Level | Primary Use in FedRAMP            | Key Controls       |
| ---------------------- | ------------- | --------------------------------- | ------------------ |
| **AWS CodeBuild**      | High          | Build service (SAST, DAST, SBOM)  | SA-11, SA-15, SI-3 |
| **AWS CodePipeline**   | High          | Deployment pipeline orchestration | CM-3, CA-7, SA-3   |
| **AWS CodeCommit**     | High          | Git repository service            | CM-3, SA-3, AU-2   |
| **AWS CodeDeploy**     | High          | Application deployment automation | CM-3, SI-7         |
| **AWS CloudFormation** | High          | Infrastructure as Code            | CM-3, SA-3, SA-10  |

---

## Backup & Disaster Recovery

| AWS Service              | FedRAMP Level | Primary Use in FedRAMP         | Key Controls      |
| ------------------------ | ------------- | ------------------------------ | ----------------- |
| **AWS Backup**           | High          | Centralized backup service     | CP-2, CP-9, SC-28 |
| **Amazon S3 Versioning** | High          | Object version history         | CP-2, CP-9, SC-28 |
| **AWS Database Backups** | High          | Automated RDS/Aurora snapshots | CP-2, CP-9, SC-28 |

---

## Networking & Content Delivery

| AWS Service                | FedRAMP Level | Primary Use in FedRAMP              | Key Controls      |
| -------------------------- | ------------- | ----------------------------------- | ----------------- |
| **Amazon CloudFront**      | High          | Content delivery network (with WAF) | SC-5, SC-7, SI-10 |
| **Elastic Load Balancing** | High          | Load balancing (ALB, NLB)           | SC-5, SC-7, SC-8  |
| **AWS Global Accelerator** | High          | Global traffic acceleration         | SC-5, SC-7        |

---

## Storage & Data Services

| AWS Service                   | FedRAMP Level | Primary Use in FedRAMP              | Key Controls           |
| ----------------------------- | ------------- | ----------------------------------- | ---------------------- |
| **Amazon S3**                 | High          | Object storage (all types)          | SC-28, SC-28(1), AU-11 |
| **Amazon EBS**                | High          | Block storage for EC2               | SC-28, SC-28(1), CP-9  |
| **Amazon EFS**                | High          | Shared file system                  | SC-28, SC-28(1)        |
| **AWS Snowball / Snowmobile** | High          | Data migration (for large datasets) | SC-28, CP-9            |

---

## Monitoring & Analytics

| AWS Service           | FedRAMP Level | Primary Use in FedRAMP                  | Key Controls            |
| --------------------- | ------------- | --------------------------------------- | ----------------------- |
| **CloudWatch**        | High          | Metrics, logs, dashboards               | CA-7, SI-4, AU-2        |
| **AWS CloudTrail**    | High          | Audit logging                           | AU-2, AU-3, AU-9, AU-11 |
| **Amazon Athena**     | High          | Query service (for VPC Flow Logs, etc.) | CA-7, SI-4              |
| **Amazon Quicksight** | Moderate      | Business intelligence and dashboards    | CA-2, SI-4              |

---

## Key Patterns for FedRAMP Architecture

### Foundation (Required)

1. **AWS Organizations** (governance)
2. **CloudTrail** (logging)
3. **AWS Config** (compliance)
4. **Security Hub** (monitoring)

### Security

5. **IAM Identity Center** (identity)
6. **KMS** (encryption keys)
7. **Secrets Manager** (credential rotation)
8. **VPC + Network Firewall** (boundary protection)

### Detection

9. **GuardDuty** (threat detection)
10. **Macie** (data classification)

### Deployment

11. **CodePipeline + CodeBuild** (CI/CD with security scanning)
12. **ECR** (container registry)
13. **ECS Fargate or EKS** (container orchestration)

### Data

14. **RDS/Aurora** (databases, encrypted)
15. **S3 + Object Lock** (logs and backups, immutable)

---

## AWS GovCloud Region Services

For **GovCloud deployments** (`us-gov-west-1`, `us-gov-east-1`), check AWS documentation for region-specific service availability. Most services listed above are available in GovCloud with identical authorization levels.

---

## Service Quotas & Limits

When building FedRAMP-aligned systems, account for:

- **CloudTrail**: Organization trail covers all accounts and regions
- **Config**: Aggregator for cross-account compliance monitoring
- **Security Hub**: Aggregation in Security account for centralized view
- **GuardDuty**: Member account delegation in Security account
- **Secrets Manager**: Auto-rotation Lambda must be region-specific

---

**Document Version:** 1.0  
**Last Updated:** 2026-05-06  
**Maintained by:** BE EASY ENTERPRISES Federal Compliance Team
