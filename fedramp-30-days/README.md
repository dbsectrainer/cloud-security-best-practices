# FedRAMP on AWS in 30 Days

**A reproducible path from a standard AWS environment to a FedRAMP-aligned posture**

This guide provides a day-by-day implementation path for federal agencies and contractors pursuing FedRAMP Moderate authorization on AWS. Each day has a concrete goal, specific AWS services, key actions, and the FedRAMP controls addressed.

---

## Week 1 (Days 1-7): Foundation & Assessment

### Day 1: AWS Organizations Multi-Account Structure
**Goal:** Establish account hierarchy for security separation  
**AWS Services:** AWS Organizations, Control Tower  
**Key Actions:**
- Create Management account (billing/governance only)
- Create Security account (security tooling, centralized logging)
- Create Log Archive account (immutable audit logs)
- Create Workload accounts (dev/staging/prod)
- Enable AWS Control Tower guardrails

**FedRAMP Controls:** AC-2, AC-3, AC-20, SC-7

---

### Day 2: CloudTrail Organization-Wide
**Goal:** Establish complete audit trail  
**AWS Services:** CloudTrail, S3, CloudWatch Logs  
**Key Actions:**
- Enable CloudTrail in all regions, all accounts
- Create S3 bucket with Object Lock (WORM) in Log Archive account
- Enable CloudTrail log file validation
- Set 7-year retention for audit logs
- Configure S3 encryption with KMS CMK

**FedRAMP Controls:** AU-2, AU-3, AU-9, AU-11

---

### Day 3: AWS Config with FedRAMP Rule Set
**Goal:** Continuous compliance monitoring  
**AWS Services:** AWS Config, Config Rules, SNS  
**Key Actions:**
- Enable AWS Config in all regions and accounts
- Deploy FedRAMP Moderate conformance pack
- Set up Config aggregator in Security account
- Create SNS notifications for non-compliant resources
- Configure Config to deliver snapshots to S3 (Log Archive account)

**FedRAMP Controls:** CA-7, CM-2, CM-6, RA-5

---

### Day 4: Security Hub + FedRAMP Standard
**Goal:** Centralized security findings and compliance scoring  
**AWS Services:** Security Hub, EventBridge, SNS  
**Key Actions:**
- Enable Security Hub with FedRAMP Best Practices standard
- Enable AWS Foundational Security Best Practices standard
- Configure cross-account aggregation in Security account
- Create EventBridge rules for CRITICAL findings → SNS
- Enable compliance score tracking

**FedRAMP Controls:** CA-2, CA-7, IR-6, RA-5

---

### Day 5: GuardDuty + Macie
**Goal:** Threat detection and data classification  
**AWS Services:** GuardDuty, Macie, S3  
**Key Actions:**
- Enable GuardDuty in all accounts and regions
- Enable Macie for S3 data classification and PII detection
- Configure GuardDuty findings to Security Hub
- Enable S3 protection and EKS audit log monitoring
- Aggregate findings in Security account

**FedRAMP Controls:** IR-4, IR-5, SI-4, SI-7

---

### Day 6: IAM Identity Center + SCPs
**Goal:** Centralized identity and access enforcement  
**AWS Services:** IAM Identity Center, AWS Organizations, SCP  
**Key Actions:**
- Enable IAM Identity Center in management account
- Configure MFA enforcement SCP (deny MFA-less access)
- Deploy deny-root-access SCP (prevent root usage)
- Deploy region restriction SCP (approve only needed regions)
- Set up permission sets aligned to least privilege roles
- Enable multi-stage approval for privileged actions

**FedRAMP Controls:** AC-2, AC-3, AC-6, IA-2, IA-5

---

### Day 7: Baseline Assessment
**Goal:** Document starting security posture  
**AWS Services:** AWS Config, Security Hub, CloudTrail  
**Key Actions:**
- Run nist_800_53_scanner against all accounts and regions
- Export Security Hub compliance score snapshot
- Document identified gaps in POA&M (Plan of Action & Milestones) template
- Identify controls implemented via inheritance from AWS
- Create evidence collection baseline

**FedRAMP Controls:** CA-2, RA-3, RA-5

---

## Week 2 (Days 8-14): Network & Access Hardening

### Day 8-9: VPC Architecture
**Goal:** Private network topology with no internet exposure  
**AWS Services:** VPC, Transit Gateway, VPC Flow Logs  
**Key Actions:**
- Design hub-and-spoke VPC topology with Transit Gateway
- All workloads in private subnets (no public IPs)
- Create VPC endpoints for all AWS services (S3, ECR, Secrets Manager, KMS, STS, CloudTrail, Config)
- Configure VPC Flow Logs to Log Archive account with CloudWatch Logs
- Enable VPC Flow Logs analysis in Athena

**FedRAMP Controls:** SC-5, SC-7, SC-7(3), AU-2

---

### Day 10: WAF + Shield
**Goal:** Application layer protection  
**AWS Services:** WAF, Shield, CloudFront, ALB  
**Key Actions:**
- Deploy AWS WAF on all CloudFront distributions and ALBs
- Enable AWS Shield Standard (automatic DDoS protection)
- Configure WAF rules: OWASP Top 10, rate limiting, IP reputation
- Enable WAF logging to S3 with 90-day retention
- Configure CloudWatch alarms for WAF blocks

**FedRAMP Controls:** SC-5, SC-7, SI-3, SI-10

---

### Day 11: PrivateLink for AWS Services
**Goal:** Eliminate internet egress for AWS API calls  
**AWS Services:** VPC Endpoints, Security Groups  
**Key Actions:**
- Create VPC endpoints for: S3, ECR, Secrets Manager, KMS, STS, CloudTrail, Config, SNS, SQS
- Update security groups to deny explicit internet egress
- Test connectivity without internet gateway
- Document endpoint usage in network diagram
- Enable endpoint policies for fine-grained access control

**FedRAMP Controls:** SC-7, SC-8, AC-17

---

### Day 12: KMS Customer Managed Keys
**Goal:** Customer-controlled encryption at rest  
**AWS Services:** KMS, CloudTrail  
**Key Actions:**
- Create CMKs for: RDS, S3 buckets (logs, application data), EBS volumes, Secrets Manager, CloudWatch Logs
- Enable automatic key rotation (annual)
- Configure key policies with least privilege (deny without explicit allow)
- Document key custodians and key purposes in SSP Appendix
- Enable CloudTrail logging for all key usage

**FedRAMP Controls:** SC-12, SC-12(1), SC-28, SC-28(1)

---

### Day 13: Secrets Manager Rotation
**Goal:** Eliminate hardcoded credentials  
**AWS Services:** Secrets Manager, IAM, Lambda  
**Key Actions:**
- Migrate all database credentials to Secrets Manager
- Configure automatic rotation (30-day rotation policy)
- Create Lambda rotation functions for custom secrets
- Audit IAM users for long-lived access keys; convert to roles
- Enable CloudTrail logging for Secrets Manager access
- Set CloudWatch alarm for access key age >90 days

**FedRAMP Controls:** IA-5, IA-5(1), SC-12

---

### Day 14: Network Firewall
**Goal:** East-west and north-south traffic inspection  
**AWS Services:** Network Firewall, Route Tables  
**Key Actions:**
- Deploy AWS Network Firewall at VPC egress points
- Configure domain allowlist for internet egress (if needed)
- Deploy DNS Firewall to block malicious domains
- Configure stateful inspection rules for internal traffic
- Enable Firewall logging to CloudWatch Logs and S3
- Document firewall rules in network architecture document

**FedRAMP Controls:** SC-7, SI-3, SI-4

---

## Week 3 (Days 15-21): Application Security

### Day 15-16: Container Security
**Goal:** Secure container supply chain  
**AWS Services:** ECR, ECS, Lambda  
**Key Actions:**
- Enable ECR image scanning (on push and continuous)
- Configure ECR lifecycle policies (retain signed images only)
- Implement Cosign image signing (verify signatures before deployment)
- Apply ECS task definition hardening: non-root user, read-only root filesystem, no privilege escalation
- Enable CloudTrail logging for image operations
- Document container security policy

**FedRAMP Controls:** CM-7, SA-10, SI-3, SI-7

---

### Day 17: SBOM Generation Pipeline
**Goal:** Software supply chain visibility  
**AWS Services:** CodeBuild, S3, Dependency-Track  
**Key Actions:**
- Add Syft to CI/CD pipeline (generate CycloneDX SBOM on every build)
- Add Grype vulnerability scanner (fail on CRITICAL CVEs)
- Archive SBOM artifacts (90-day retention minimum)
- Upload SBOMs to Dependency-Track for continuous monitoring
- Create Makefile targets for local SBOM generation
- Document SBOM generation process in CONTRIBUTING.md

**FedRAMP Controls:** SA-12, SR-3, SR-4, SI-2

---

### Day 18: SAST/DAST in CI/CD
**Goal:** Shift-left security scanning  
**AWS Services:** CodeBuild, CodePipeline  
**Key Actions:**
- Add Semgrep SAST to pull request checks (fail on HIGH findings)
- Add OWASP ZAP DAST to staging deployment pipeline
- Configure CodeBuild to fail on HIGH/CRITICAL findings
- Create remediation runbooks for common findings
- Document scanning results in SSP SA-11 evidence
- Enable code quality gate (max 5% technical debt)

**FedRAMP Controls:** SA-11, SA-15, SI-3

---

### Day 19: API Gateway Hardening
**Goal:** Secure API endpoints  
**AWS Services:** API Gateway, WAF, CloudTrail  
**Key Actions:**
- Enable API Gateway WAF attachment
- Configure API throttling and quotas per identity
- Enable API access logging to CloudWatch Logs
- Add API key and OAuth 2.0 authentication enforcement
- Configure mutual TLS (mTLS) for service-to-service APIs
- Enable CloudTrail logging for API management plane

**FedRAMP Controls:** AC-17, SC-8, SI-10

---

### Day 20: Cognito MFA + Federation
**Goal:** Strong user authentication  
**AWS Services:** Cognito, IAM Identity Center  
**Key Actions:**
- Enable Cognito MFA (TOTP or SMS; TOTP preferred)
- Configure OIDC federation with agency IdP (Active Directory, Okta, etc.)
- Set password policy: minimum 12 characters, complexity, 90-day rotation
- Enable Cognito advanced security features (anomaly detection, compromised credentials)
- Configure account lockout after 5 failed attempts
- Enable CloudTrail logging for authentication events

**FedRAMP Controls:** IA-2, IA-2(1), IA-2(12), IA-5

---

### Day 21: Penetration Test Scheduling
**Goal:** Independent security validation  
**AWS Services:** None (external service)  
**Key Actions:**
- Engage approved FedRAMP penetration test firm
- Define scope: external, internal, web application, API, infrastructure
- Identify rules of engagement and authorized testing windows
- Schedule test for Day 25-27
- Prepare test coordination documentation
- Establish incident response contact list

**FedRAMP Controls:** CA-2, CA-8, RA-5

---

## Week 4 (Days 22-30): Compliance Documentation & ATO Prep

### Day 22: System Security Plan Template
**Goal:** SSP document skeleton  
**Key Actions:**
- Download FedRAMP SSP template from fedramp.gov
- Populate system description (purpose, data types, boundaries)
- Complete system inventory table (AWS services, versions)
- Document data flows (ingress, processing, egress)
- Map all controls to implementation status
- Create appendices structure (evidence references)

---

### Day 23-24: Control Implementation Documentation
**Goal:** Evidence for each NIST 800-53 Moderate control  
**Key Actions:**
- For each of 325 Moderate baseline controls: document what implements it
- Identify: customer-responsible vs. AWS-inherited vs. shared controls
- Reference specific CloudTrail logs, Config rule names, IAM policies as evidence
- Create screenshot evidence (Security Hub compliance, Config conformance)
- Document AWS inheritance controls per FedRAMP documentation
- Complete Appendix A (control summary matrix)

---

### Day 25: POA&M for Gaps
**Goal:** Document and track open findings  
**Key Actions:**
- Create POA&M for each gap identified in Day 7 baseline
- Assign owners, due dates, and milestones for each item
- Prioritize by risk level (CRITICAL, HIGH, MEDIUM, LOW)
- Estimate effort and resource requirements
- Schedule remediation sprints (e.g., 2-week cycles)
- Establish weekly POA&M review cadence

---

### Day 26: Incident Response Plan
**Goal:** FISMA IR documentation  
**Key Actions:**
- Complete FedRAMP Incident Response Plan template
- Define roles (incident commander, communications, forensics, remediation)
- Create escalation paths and contact list
- Document containment and recovery procedures
- Define notification timeline (1 hour to federal agency)
- Schedule tabletop exercise for Day 29

---

### Day 27: Contingency Plan
**Goal:** CP documentation and testing  
**Key Actions:**
- Document Recovery Time Objectives (RTO) per system component
- Document Recovery Point Objectives (RPO) per data type
- Complete Business Impact Analysis (BIA)
- Document backup and restore procedures
- Test restore from backup (document results as CP evidence)
- Verify backup integrity and encryption

---

### Day 28: Evidence Collection Automation
**Goal:** Automate ATO evidence gathering  
**AWS Services:** Config, Security Hub, CloudWatch, EventBridge, S3  
**Key Actions:**
- Schedule Config snapshot exports (weekly to S3)
- Schedule Security Hub compliance reports (monthly)
- Create S3 bucket for ATO evidence archive with versioning
- Automate CloudWatch dashboard export for monitoring evidence
- Create Lambda function to export compliance reports
- Set up SNS notifications for evidence collection failures

---

### Day 29: Internal Readiness Review
**Goal:** Pre-3PAO self-assessment  
**Key Actions:**
- Complete FedRAMP readiness assessment questionnaire
- Review all SSP sections for completeness and accuracy
- Verify all POA&M items have owners and realistic dates
- Conduct internal tabletop for incident response
- Perform self-assessment against FedRAMP baseline controls
- Document any new findings or gaps

---

### Day 30: 3PAO Engagement Kickoff
**Goal:** Start independent assessment  
**Key Actions:**
- Submit kickoff package to selected 3PAO (Third Party Assessor Organization)
- Provide system description and boundary documentation
- Share SSP draft and appendices for initial review
- Grant 3PAO access to AWS accounts and systems (read-only)
- Schedule assessment kick-off call and weekly review meetings
- Establish communication protocols and escalation paths

---

## Success Criteria

At Day 30, you should have:

- [ ] Security Hub FedRAMP conformance pack showing >85% compliance
- [ ] CloudTrail enabled across all accounts and regions with WORM logs
- [ ] All data encrypted at rest (KMS CMKs) and in transit (TLS 1.2+)
- [ ] MFA enforced for all human access (100% coverage)
- [ ] No public-facing resources without WAF protection
- [ ] SBOM generated for all container images with 0 CRITICAL CVEs
- [ ] SSP draft completed with all 325 Moderate controls documented
- [ ] POA&M populated with all identified gaps assigned and dated
- [ ] IR and CP plans documented and tested
- [ ] 3PAO engaged and baseline assessment started

---

## AWS Services Checklist

- [ ] AWS Organizations + Control Tower
- [ ] CloudTrail (organization-wide, all regions)
- [ ] AWS Config + Config Rules
- [ ] Security Hub
- [ ] GuardDuty + Macie
- [ ] IAM Identity Center + SCPs
- [ ] VPC + Transit Gateway
- [ ] WAF + Shield
- [ ] Network Firewall
- [ ] VPC Endpoints (all critical services)
- [ ] KMS (CMKs for all data at rest)
- [ ] Secrets Manager
- [ ] ECR with image scanning
- [ ] API Gateway (WAF, logging)
- [ ] Cognito (MFA, federation)

---

## Key Contacts & Resources

**FedRAMP Marketplace:** https://marketplace.fedramp.gov/  
**FedRAMP SSP Template:** https://www.fedramp.gov/templates/  
**AWS GovCloud:** https://aws.amazon.com/govcloud-us/  
**NIST 800-53 Rev 5:** https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf  
**AWS FedRAMP Compliance:** https://aws.amazon.com/compliance/fedramp/  

---

**Document Version:** 1.0  
**Last Updated:** 2026-05-06  
**Maintained by:** BE EASY ENTERPRISES Federal Compliance Team
