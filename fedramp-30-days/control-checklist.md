---
title: FedRAMP Control Checklist
---

# FedRAMP Moderate Control Checklist

This checklist is organized by implementation phase and maps each action to the corresponding NIST 800-53 Moderate baseline control.

---

## Phase 1: Foundation & Assessment (Days 1-7)

### Multi-Account & Governance (Day 1)

- [ ] AC-2: Account Management — AWS Organizations structure
- [ ] AC-3: Access Enforcement — SCP policies in place
- [ ] AC-20: Use of External Information Systems — Multi-account isolation
- [ ] SC-7: Boundary Protection — Account boundaries defined

### Audit & Logging (Day 2)

- [ ] AU-2: Audit Events — CloudTrail enabled all regions
- [ ] AU-3: Content of Audit Records — CloudTrail log format verified
- [ ] AU-9: Protection of Audit Information — S3 Object Lock enabled
- [ ] AU-11: Audit Record Retention — 7-year retention configured
- [ ] SC-28(1): Cryptographic Protection — Logs encrypted at rest

### Configuration Management (Day 3)

- [ ] CA-7: Continuous Monitoring — AWS Config enabled
- [ ] CM-2: Baseline Configuration — Config conformance pack deployed
- [ ] CM-6: Configuration Settings — FedRAMP rules active
- [ ] RA-5: Vulnerability Scanning — Automated scanning enabled

### Compliance Monitoring (Day 4)

- [ ] CA-2: Security Assessments — Security Hub enabled
- [ ] CA-7: Continuous Monitoring — Compliance scoring active
- [ ] IR-6: Incident Reporting — CRITICAL findings → SNS
- [ ] RA-5: Vulnerability Monitoring — Hub aggregates findings

### Threat Detection (Day 5)

- [ ] IR-4: Incident Handling — GuardDuty findings processed
- [ ] IR-5: Incident Monitoring — Dashboard configured
- [ ] SI-4: Information System Monitoring — Macie enabled
- [ ] SI-7: Software, Firmware, Information Integrity Verification

### Identity & Access (Day 6)

- [ ] AC-2: Account Management — IdC user/group management
- [ ] AC-3: Access Enforcement — Permission sets configured
- [ ] AC-6: Least Privilege — Role-based access control
- [ ] IA-2: Authentication — MFA enforced via SCP
- [ ] IA-5: Authentication Mechanisms — Password policy set

### Baseline Assessment (Day 7)

- [ ] CA-2: Security Assessments — Baseline scan completed
- [ ] RA-3: Risk Assessment — POA&M gaps documented
- [ ] RA-5: Vulnerability Scanning — Baseline established

---

## Phase 2: Network & Access Hardening (Days 8-14)

### VPC Architecture (Days 8-9)

- [ ] SC-5: Denial of Service Protection — Transit Gateway redundancy
- [ ] SC-7: Boundary Protection — Private subnets for all workloads
- [ ] SC-7(3): Access Points — VPC endpoints for AWS APIs
- [ ] AU-2: Audit Events — VPC Flow Logs enabled

### Application Protection (Day 10)

- [ ] SC-5: Denial of Service Protection — WAF rules active
- [ ] SC-7: Boundary Protection — WAF on all entry points
- [ ] SI-3: Malicious Code Protection — Rate limiting enabled
- [ ] SI-10: Information System Monitoring — Blocked requests logged

### AWS Service Access (Day 11)

- [ ] SC-7: Boundary Protection — VPC endpoints configured
- [ ] SC-8: Transmission Confidentiality — Endpoint encryption enforced
- [ ] AC-17: Remote Access — PrivateLink eliminates internet gateway

### Encryption at Rest (Day 12)

- [ ] SC-12: Cryptographic Key Establishment & Management
- [ ] SC-12(1): Cryptographic Key Protection — Key rotation enabled
- [ ] SC-28: Protection of Information at Rest — CMKs for all services
- [ ] SC-28(1): Cryptographic Protection — Key policies configured

### Secrets Management (Day 13)

- [ ] IA-5: Authentication Mechanisms — Secrets Manager enabled
- [ ] IA-5(1): Password-Based Authentication — Rotation configured
- [ ] SC-12: Cryptographic Key Establishment — Secrets encrypted

### Network Inspection (Day 14)

- [ ] SC-7: Boundary Protection — Firewall rules configured
- [ ] SI-3: Malicious Code Protection — Domain allowlisting
- [ ] SI-4: Information System Monitoring — DNS filtering enabled

---

## Phase 3: Application Security (Days 15-21)

### Container Image Security (Days 15-16)

- [ ] CM-7: Least Functionality — Signed images only
- [ ] SA-10: Developmental Activities — Image scanning on push
- [ ] SI-3: Malicious Code Protection — Cosign signature verification
- [ ] SI-7: Software, Firmware Integrity — Task hardening applied

### Software Supply Chain (Day 17)

- [ ] SA-12: Supply Chain Protection — SBOM generation
- [ ] SR-3: Supply Chain Risk Management — Vulnerability scanning
- [ ] SR-4: Supplier Contingency Planning — Dependency tracking
- [ ] SI-2: Flaw Remediation — CRITICAL CVE detection

### Code Security (Day 18)

- [ ] SA-11: Developer-Initiated Security Testing — SAST enabled
- [ ] SA-15: Development Process, Standards, Tools — DAST in pipeline
- [ ] SI-3: Malicious Code Protection — Fail-safe defaults

### API Security (Day 19)

- [ ] AC-17: Remote Access — API authentication required
- [ ] SC-8: Transmission Confidentiality — TLS 1.2+ enforced
- [ ] SI-10: Information System Monitoring — Access logging enabled

### User Authentication (Day 20)

- [ ] IA-2: Authentication — MFA mandatory
- [ ] IA-2(1): Authentication — Multi-factor authentication
- [ ] IA-2(12): Cryptographic-Based Authentication
- [ ] IA-5: Authentication Mechanisms — Password policy enforced

### Penetration Testing (Day 21)

- [ ] CA-2: Security Assessments — 3PAO pentest scheduled
- [ ] CA-8: Security Function as a Service — External assessment
- [ ] RA-5: Vulnerability Scanning — Third-party validation

---

## Phase 4: Documentation & ATO (Days 22-30)

### System Documentation (Day 22)

- [ ] CA-2: Security Assessments — SSP structure complete
- [ ] RA-3: Risk Assessment — System boundaries documented
- [ ] SA-1: System Development Life Cycle — SDLC documented

### Control Implementation Mapping (Days 23-24)

- [ ] CA-2: Security Assessments — All 325 controls documented
- [ ] SA-3: System Development Life Cycle — Evidence collected
- [ ] Document AWS-inherited controls per FedRAMP documentation
- [ ] Create screenshot evidence for all controls

### POA&M Tracking (Day 25)

- [ ] CA-2: Security Assessments — POA&M created
- [ ] RA-3: Risk Assessment — Gaps prioritized by risk
- [ ] Milestones and owners assigned for each item

### Incident Response (Day 26)

- [ ] IR-1: Incident Response Policy — IR plan documented
- [ ] IR-2: Incident Response Training — Roles and contacts defined
- [ ] IR-4: Incident Handling — Procedures documented

### Business Continuity (Day 27)

- [ ] CP-1: Contingency Planning Policy — Plan documented
- [ ] CP-2: Contingency Plan — RTO/RPO defined
- [ ] CP-4: Contingency Plan Testing — Backup restore tested

### Evidence Automation (Day 28)

- [ ] CA-7: Continuous Monitoring — Automated evidence collection
- [ ] SI-4: Information System Monitoring — Audit trail maintained
- [ ] Reports scheduled for executive review

### Readiness Review (Day 29)

- [ ] CA-2: Security Assessments — Internal assessment complete
- [ ] RA-3: Risk Assessment — Findings documented
- [ ] IR-1: Incident Response — Tabletop exercise conducted

### 3PAO Engagement (Day 30)

- [ ] CA-2: Security Assessments — 3PAO engaged
- [ ] RA-3: Risk Assessment — Assessment scheduled
- [ ] Access granted to auditors

---

## NIST 800-53 Moderate Baseline Summary

**Total Controls:** 325 (across 20 control families)

| Family | Short Name                                       | Count | Checklist Coverage |
| ------ | ------------------------------------------------ | ----- | ------------------ |
| AC     | Access Control                                   | 22    | ✓                  |
| AT     | Awareness and Training                           | 4     | ✓                  |
| AU     | Audit and Accountability                         | 13    | ✓                  |
| CA     | Assessment, Authorization, Continuous Monitoring | 9     | ✓                  |
| CM     | Configuration Management                         | 10    | ✓                  |
| CP     | Contingency Planning                             | 13    | ✓                  |
| IA     | Identification and Authentication                | 8     | ✓                  |
| IR     | Incident Response                                | 10    | ✓                  |
| MA     | Maintenance                                      | 7     | ✓                  |
| MP     | Media Protection                                 | 8     | ✓                  |
| PE     | Physical and Environmental Protection            | 15    | ✓                  |
| PL     | Planning                                         | 11    | ✓                  |
| PS     | Personnel Security                               | 8     | ✓                  |
| RA     | Risk Assessment                                  | 5     | ✓                  |
| SA     | System and Services Acquisition                  | 16    | ✓                  |
| SC     | System and Communications Protection             | 40    | ✓                  |
| SI     | System and Information Integrity                 | 14    | ✓                  |

---

**Document Version:** 1.0  
**Last Updated:** 2026-05-06  
**Maintained by:** BE EASY ENTERPRISES Federal Compliance Team
