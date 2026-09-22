---
title: Tech Stack Update Plan
layout: default
---

# 2026 Tech Stack Update Plan

## Purpose

This document is the output of a full-repository review conducted in September 2026 to identify content that has drifted out of date with the current cloud security tooling and regulatory ecosystem. Most files carry a "2025-2026" label, but several product names, version numbers, and framework citations are now factually stale or refer to products that have been renamed, merged, or acquired. This plan catalogs those findings and sequences the fixes so the repository's "current as of 2026" claim (README.md line 197) is actually true.

No content changes are made in this commit — this is the review and plan only, ready for the team to execute or for a follow-up PR per phase below.

---

## Findings

### 1. Vendor/product renames and mergers (factually incorrect as written)

| Issue | Why it's stale | Locations | Suggested replacement |
| --- | --- | --- | --- |
| **Azure AD** / **Azure Active Directory** | Microsoft completed the rebrand to **Microsoft Entra ID** in 2023; "Azure AD" has not been the product's name for several years. | `README.md:83`, `IMPLEMENTATION_GUIDE.md:173`, `index.html:323,329` | Replace with "Microsoft Entra ID" (first mention can note "formerly Azure AD" once for reader continuity). |
| **Twistlock** | Twistlock was acquired by Palo Alto Networks and fully folded into **Prisma Cloud Compute** by 2020. The standalone brand no longer exists. | `IMPLEMENTATION_GUIDE.md:50`, `TESTING_GUIDE.md:146`, `README.md:88` | Replace "Twistlock/Prisma Cloud" with "Prisma Cloud Compute". |
| **Bridgecrew** | Bridgecrew was acquired by Palo Alto Networks in 2021 and merged into **Prisma Cloud** (its code-to-cloud/IaC scanning capability); it is no longer sold as a separate product. | `IMPLEMENTATION_GUIDE.md:58,152`, `TESTING_GUIDE.md:160`, `README.md:87` | Replace "Bridgecrew" with "Prisma Cloud (code-to-cloud)" or drop the standalone mention. |
| **Chronicle** (standalone) | Google rebranded Chronicle as **Google Security Operations (Google SecOps)** in 2024, integrating it with Mandiant capabilities. | `IMPLEMENTATION_GUIDE.md:47`, `SECURITY_FRAMEWORK.md:200,206`, `README.md:84`, `index.html:351,357` | Replace "Chronicle" with "Google Security Operations (Google SecOps)". |
| **Lacework** | Acquired by Fortinet in late 2024; it's now part of the Fortinet CNAPP portfolio (FortiCNAPP), not an independent vendor. | `IMPLEMENTATION_GUIDE.md:48,154`, `SECURITY_FRAMEWORK.md:209`, `README.md:86`, `TESTING_GUIDE.md:157` | Replace "Lacework" with "Fortinet Lacework (FortiCNAPP)" or drop from the independent-vendor list. |
| **HashiCorp Sentinel / Terraform** ownership | IBM completed its acquisition of HashiCorp in 2025; Terraform/Sentinel/Vault are now IBM-owned products. Also, HashiCorp's 2023 BSL relicensing spawned **OpenTofu** (now a Linux Foundation project) as the open-source Terraform fork many teams adopted instead. | `README.md:72`, `IMPLEMENTATION_GUIDE.md:37,54`, `COMPLIANCE.md:123` | Note IBM ownership where HashiCorp is named, and add OpenTofu as an alternative/mention in the IaC tooling list. |
| **"GPT-powered analysis"** | Vendor- and model-specific phrasing that reads as a stale 2023-era buzzword rather than a durable architectural description. | `SECURITY_FRAMEWORK.md:151` | Reword to vendor-neutral language, e.g., "LLM-powered security orchestration" or "generative-AI-assisted analysis." |

### 2. Version/standard references that have moved on

| Issue | Current state (Sept 2026) | Locations | Suggested update |
| --- | --- | --- | --- |
| **PCI-DSS v4.0** | Superseded by **PCI-DSS v4.0.1** (June 2024); the v4.0 future-dated requirements became mandatory March 31, 2025, and are now simply "current requirements," not a future milestone. | 10 occurrences across `README.md`, `SECURITY_FRAMEWORK.md`, `COMPLIANCE.md`, `TESTING_GUIDE.md` (heading only, body already generic), `VENDOR_SECURITY_ASSESSMENT.md`, `SECURITY_TRAINING_GUIDE.md`, `index.html` | Update every "PCI-DSS v4.0" reference to "PCI-DSS v4.0.1" and drop "future-dated"/"enhanced requirements" framing since those requirements are already in force. |
| **Terraform "v1.6+"** | Terraform has advanced multiple minor versions since 1.6 (released Oct 2023); pinning to 1.6 undersells current capability and predates the OpenTofu fork entirely. | `IMPLEMENTATION_GUIDE.md:37` | Update to a current baseline (e.g., "Terraform 1.9+ / OpenTofu 1.8+") rather than a hardcoded old minimum. |
| **Post-quantum cryptography** references are vague | NIST finalized the first PQC standards in **August 2024**: FIPS 203 (ML-KEM), FIPS 204 (ML-DSA), FIPS 205 (SLH-DSA). The repo only says "quantum-resistant"/"post-quantum" without citing the now-final standards. | `SECURITY_FRAMEWORK.md:119`, `INNOVATION.md` (Quantum-Resistant Security Transition section), `RISK_MANAGEMENT.md` (Quantum Computing Threats section), `VENDOR_SECURITY_ASSESSMENT.md` | Cite FIPS 203/204/205 explicitly and reframe "planning for" as "migrating to," since the standards are final and agencies (per NIST/CISA/OMB guidance) are now in active migration windows. |
| **OWASP Top 10 2024** | `SECURITY_TRAINING_GUIDE.md:87` cites "OWASP Top 10 2024" for web app security — the current published edition is still **OWASP Top 10:2021**; 2024 is not a released edition. For the AI-specific training content nearby, the relevant and actively maintained list is the **OWASP Top 10 for LLM Applications** (2025 edition). | `SECURITY_TRAINING_GUIDE.md:87` | Correct to "OWASP Top 10:2021" for web apps, and add "OWASP Top 10 for LLM Applications (2025)" given the AI-security emphasis of that section. |
| **EU AI Act** cited without its phased timeline | The Act entered into force Aug 2024. Key dates: prohibited-practice ban (Feb 2025, already passed), GPAI model obligations (Aug 2025, already passed), high-risk system obligations (Aug 2026 — imminent/current as of this review). The repo cites the Act only generically. | `README.md`, `SECURITY_FRAMEWORK.md`, `COMPLIANCE.md`, `RISK_MANAGEMENT.md`, `VENDOR_SECURITY_ASSESSMENT.md`, `SECURITY_TRAINING_GUIDE.md` | Add the phased compliance timeline so readers know which obligations are already live vs. upcoming as of late 2026. |
| **Ruby/Jekyll toolchain** | `Gemfile` pins `jekyll "~> 4.3.0"`. Should be verified against the latest stable Jekyll release before the plan is executed, and `bundle outdated` should be run as part of implementation to catch any other stale gems (webrick, kramdown-parser-gfm, etc.). | `Gemfile` | Run `bundle outdated` and bump pinned versions as part of Phase 4 below (low risk, mechanical). |

### 3. Structural/copy issues found during the review (not tech-stack, but worth fixing alongside)

- `SECURITY_FRAMEWORK.md` has a duplicated `## Compliance and Governance` heading (lines 159 and 161) and a duplicated `## Technology Integration` heading (lines 192 and 194) — leftover from a prior edit pass.
- `.github/copilot-instructions.md` still describes the docs as needing review ("Please review and let me know...") — this looks like unfinished boilerplate rather than a finished instructions file.
- Several files repeat the same generic bullet content across README.md, SECURITY_FRAMEWORK.md, COMPLIANCE.md, and IMPLEMENTATION_GUIDE.md (e.g., the compliance framework list appears near-verbatim in four places). Not urgent, but worth flagging so an update to one doesn't silently miss the other three.

---

## Remediation Plan

Work is sequenced so that objective, low-risk factual corrections land first, and interpretive/content-judgment updates land later with review.

### Phase 1 — Factual vendor/product corrections (low risk, mechanical)
Find-and-replace across all affected files:
- Azure AD → Microsoft Entra ID
- Twistlock/Prisma Cloud → Prisma Cloud Compute
- Bridgecrew → Prisma Cloud (code-to-cloud) or removed from standalone lists
- Chronicle → Google Security Operations (Google SecOps)
- Lacework → Fortinet Lacework (FortiCNAPP), or removed from "independent vendor" framing
- PCI-DSS v4.0 → PCI-DSS v4.0.1 (all 10 occurrences)

**Effort:** ~1-2 hours. **Risk:** minimal — these are pure fact corrections with no architectural implications.

### Phase 2 — Version/standards currency updates
- Terraform version baseline in `IMPLEMENTATION_GUIDE.md`; add OpenTofu as a named alternative in the IaC tooling section.
- Add FIPS 203/204/205 citations wherever "quantum-resistant"/"post-quantum" appears.
- Fix the OWASP Top 10 citation in `SECURITY_TRAINING_GUIDE.md` and add the OWASP LLM Top 10 (2025).
- Add the EU AI Act phased-obligation timeline (prohibited practices Feb 2025, GPAI Aug 2025, high-risk Aug 2026) to the compliance-facing docs.
- Reword "GPT-powered analysis" to vendor-neutral phrasing in `SECURITY_FRAMEWORK.md`.

**Effort:** ~2-3 hours, mostly writing 2-3 sentence additions. **Risk:** low — additive and clarifying, doesn't remove existing claims.

### Phase 3 — Structural cleanup
- De-duplicate the repeated headings in `SECURITY_FRAMEWORK.md`.
- Finish or replace the placeholder closing line in `.github/copilot-instructions.md`.
- Consider consolidating the four near-duplicate "compliance frameworks covered" lists into one canonical source (e.g., keep the full version in `COMPLIANCE.md` and have README/SECURITY_FRAMEWORK/IMPLEMENTATION_GUIDE link to it instead of repeating it) to prevent future drift.

**Effort:** ~1 hour.

### Phase 4 — Toolchain hygiene
- Run `bundle outdated` against `Gemfile`/`Gemfile.lock` and bump Jekyll and plugin gems to current stable releases; re-run `bundle exec jekyll build` to confirm a clean build afterward.

**Effort:** ~30 minutes plus a build verification.

### Suggested execution order
Phase 1 → Phase 2 → Phase 4 (mechanical, easy to batch and verify) → Phase 3 (lowest urgency, cosmetic).

---

## Out of Scope / Not Flagged

The `fedramp-30-days/` directory (control checklist, AWS services reference, 30-day roadmap) was reviewed and found to be internally consistent and grounded in real, currently-valid AWS service names and NIST 800-53 control IDs — no stale product names were found there. It already carries an explicit disclaimer to check `fedramp.gov/marketplace` for current authorization status, which is the right pattern; no changes recommended.

---

**Document Version:** 1.0 | **Prepared:** 2026-09-22
