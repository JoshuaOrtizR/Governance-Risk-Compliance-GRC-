# ISO/IEC 27001 Portfolio (2022)
## Technical Playbook (ISO/IEC 27001:2022 & ISO/IEC 27002:2022)

**Focus areas:** Asset Management, Access Control, Risk Assessment, Business Continuity / ICT Readiness  
**Prepared by:** Joshua Ortiz  
**Date:** 2026-01-06  

> **Note:** This is **not** an official copy of ISO standards and does **not** reproduce ISO copyrighted text.  
> This document is intended to demonstrate **practical understanding**, **implementation thinking**, and **evidence collection** for an Information Security Management System (ISMS).

---

## Document control

- **Owner:** Joshua Ortiz  
- **Classification:** Internal  

### Revision history

| Version | Date       | Author        | Change summary   |
|--------:|------------|---------------|------------------|
| 0.1     | 2026-01-18 | Joshua Ortiz  | Initial draft    |

---

## How to use this document

1. Pick a small scope:
   - Home lab
   - Small company scenario
   - Cloud tenant (e.g., AWS/Azure/GCP / M365 / Google Workspace)

2. Fill the templates in the appendices with **real examples**:
   - Assets
   - Risks
   - Access roles and approvals
   - Continuity objectives (RTO/RPO)

3. Collect evidence:
   - Screenshots
   - Tickets (service desk / change mgmt)
   - Exports (IAM groups, MDM inventory, cloud inventory)
   - Config snippets
   - Logs

4. Keep your report **audit-style**:
   - What you did
   - How you did it
   - How you can prove it works

---

# 1. ISO/IEC 27001 (portfolio context)

ISO/IEC 27001 is a requirements standard for establishing, implementing, maintaining, and continually improving an **Information Security Management System (ISMS)**.

**Key idea:** ISO 27001 is **risk-based**. You assess information security risks and select controls (often from **Annex A**) as risk treatment.

### What you should be able to show in a portfolio
- **Scope definition** (what is in/out of your ISMS)
- **Risk assessment** and **risk treatment** approach (repeatable and consistent)
- **Statement of Applicability (SoA)**: which Annex A controls you apply and why
- Documented policies/procedures (where appropriate) and **operational evidence** they are implemented
- Monitoring, internal audit, management review, and continual improvement artifacts

### ISO 27001 structure (high level)
- Clauses **4–10** contain mandatory ISMS requirements (context, leadership, planning, support, operation, performance evaluation, improvement).
- **Annex A** provides a catalogue of controls (93 in ISO/IEC 27001:2022) to consider for risk treatment.
- ISO/IEC **27002:2022** provides guidance on implementing Annex A controls.

---

# 2. Information security risk assessment and treatment

### Relevant ISO/IEC 27001 requirements (typical mapping)
- **Clause 6.1.2** — Information security risk assessment process  
- **Clause 6.1.3** — Information security risk treatment  

---

## 2.1 Risk assessment workflow (technical, repeatable)

1. **Define scope and boundaries**
   - Systems, processes, locations, suppliers/third parties

2. **Define risk criteria**
   - Risk appetite/tolerance
   - Impact areas (confidentiality, integrity, availability, legal/regulatory, financial, reputation)
   - Likelihood scale and scoring rules

3. **Build asset/process list**
   - Assets/services are the inputs for risk identification

4. **Identify risk scenarios**
   - Threat source + threat event + vulnerability/predisposing condition

5. **Assess likelihood and impact**
   - Compute **inherent risk** (before controls)

6. **Select treatment option**
   - Avoid / Reduce (Mitigate) / Share (Transfer) / Accept

7. **Choose controls**
   - Create a **Risk Treatment Plan (RTP)** mapping controls → actions → owners → due dates

8. **Estimate residual risk**
   - Re-score after treatment and record residual risk

9. **Record risk acceptance**
   - Who accepted it, when, and why

10. **Create/maintain the SoA**
   - Which controls are applicable and the justification for inclusion/exclusion

11. **Track and reassess**
   - Periodically and whenever there is a major change

---

## 2.2 Example risk rating model

A simple model is:

**Risk Score = Likelihood (1–5) × Impact (1–5) → 1–25**

### Likelihood × Impact matrix (example)

| Likelihood \ Impact | 1 | 2 | 3 | 4 | 5 |
|---:|---:|---:|---:|---:|---:|
| **1** | 1 | 2 | 3 | 4 | 5 |
| **2** | 2 | 4 | 6 | 8 | 10 |
| **3** | 3 | 6 | 9 | 12 | 15 |
| **4** | 4 | 8 | 12 | 16 | 20 |
| **5** | 5 | 10 | 15 | 20 | 25 |

### Suggested thresholds (example)
- **1–5:** Low (accept or minor improvement)
- **6–12:** Medium (treat with planned improvements)
- **13–25:** High (treat urgently; management attention)

---

## 2.3 Portfolio artifacts for risk management

- Risk assessment methodology document (how you score, how often you reassess)
- Risk register with owners, dates, and evidence links
- Statement of Applicability (SoA) with inclusion/exclusion rationale for Annex A controls
- Risk Treatment Plan (RTP) mapped to tasks/tickets and target dates
- Risk acceptance records (who accepted, when, and why)
- Periodic re-assessment notes (change-driven or scheduled)

---

# 3. Asset management (information + systems + supporting assets)

### Typical ISO/IEC 27001 Annex A controls to reference in a portfolio
- **A.5.9** Inventory of information and other associated assets  
- **A.5.10** Acceptable use of information and other associated assets  
- **A.5.11** Return of assets  
- **A.5.12** Classification of information  
- **A.5.13** Labelling of information  
- **A.5.14** Information transfer  

---

## 3.1 Asset inventory (what “good” looks like)

A strong asset inventory is:

- **Complete for the defined scope**
  - Covers information assets **and** the assets that store/process/transmit them (endpoints, servers, SaaS, cloud resources, removable media)

- **Ownership defined**
  - Every asset has an owner accountable for classification and protection

- **Classification applied**
  - Labels and handling rules are consistent with your classification scheme

- **Lifecycle-aware**
  - Onboarding/change/decommission steps update the inventory

- **Integrated with operations**
  - CMDB or spreadsheet + ticketing, MDM, cloud inventory, procurement, and offboarding workflows

---

## 3.2 Sample classification scheme (example)

Keep the scheme simple and enforceable.

- **Public** — approved for public release  
- **Internal** — business info for employees/contractors  
- **Confidential** — could harm the organization if disclosed (customer data, contracts)  
- **Restricted** — highest sensitivity (credentials, encryption keys, regulated data)  

---

## 3.3 Sample asset register excerpt (template)

Maintain this in a spreadsheet/CMDB. Include an excerpt in your portfolio and explain how it stays updated.

| Asset ID | Asset / Data set     | Type         | Owner                | Classification | Notes / key controls |
|---------:|-----------------------|--------------|----------------------|----------------|----------------------|
| A-001    | Customer database     | Database     | Data Owner – Sales Ops | Restricted   | Encryption at rest; MFA for admins; daily backups; audit logging |
| A-002    | HR share drive        | File storage | Data Owner – HR      | Confidential  | DLP labels; least-privilege groups; retention policy |
| A-003    | Corporate laptops     | Endpoints    | IT Operations        | Internal      | MDM enforced; full-disk encryption; patch SLAs |

---

## 3.4 Evidence to collect (audit-style)

- Export/screenshot of asset inventory (owners + classification shown)
- Procedure: asset onboarding/change/removal (and how inventory is updated)
- Example: decommission record showing secure disposal and data deletion
- Example: acceptable use policy acknowledgement (training record or signed form)

---

# 4. Access control (IAM + technical enforcement)

### Typical ISO/IEC 27001 Annex A controls to reference
- **A.5.15** Access control (topic-specific policy and rules)  
- **A.5.16** Identity management  
- **A.5.17** Authentication information  
- **A.5.18** Access rights  
- **A.8.2** Privileged access rights  
- **A.8.3** Information access restriction  
- **A.8.5** Secure authentication  

---

## 4.1 Core principles you should show

- **Least privilege:** only what’s needed, nothing more  
- **Need-to-know:** restrict data access to justified roles  
- **Separation of duties:** avoid one person controlling end-to-end risky actions  
- **Strong authentication:** MFA where possible; protect authentication secrets  
- **Accountability:** unique user IDs; logging/monitoring for access events  

---

## 4.2 Joiner–Mover–Leaver (JML) lifecycle (example)

Define a standard workflow enforced by IAM + HR + ticketing.

- **Joiner**
  - Create identity → assign baseline roles → issue device → enforce MFA → record policy acceptance

- **Mover**
  - Role change ticket → remove old access first (or same day) → grant new access → log approvals

- **Leaver**
  - Disable identity → revoke sessions/tokens → remove group memberships → recover assets → confirm data return and account closures

---

## 4.3 Access request + approval (template excerpt)

| Field | Example | Required? | Notes |
|------|---------|----------:|------|
| Requestor | j.smith | Yes | Unique identity (no shared accounts) |
| Target system | AWS prod account | Yes | Specify environment (dev/test/prod) |
| Role / permission set | ReadOnlyAccess | Yes | Use RBAC/permission sets, not ad-hoc grants |
| Business justification | On-call rotation for service X | Yes | Must be auditable |
| Approver | System Owner / Manager | Yes | Approver cannot be the requestor |
| Duration | 14 days | Recommended | Temporary access by default for elevated roles |
| Ticket/record ID | AC-2026-0012 | Yes | Single source of truth |

---

## 4.4 Privileged access (PAM) — technical controls you can demonstrate

- Separate admin accounts; no admin rights on daily-use accounts
- Just-in-time (JIT) elevation and time-bound role activation (where supported)
- MFA enforced for privileged actions; strong session controls
- Privileged session logging; command auditing (where possible)
- Quarterly access reviews for privileged groups and critical systems

---

## 4.5 Evidence to collect (audit-style)

- Access control policy + authentication policy
- Screenshots/exports:
  - Group memberships
  - Role assignments
  - MFA enforcement dashboard
- Access review evidence:
  - List of privileged accounts + review sign-off
- Sample joiner/leaver tickets with timestamps and approvals (redact personal data)
- Audit logs:
  - Sign-in logs
  - Admin action logs
  - Alerting rules (e.g., impossible travel, risky sign-in)

---

# 5. Business continuity and ICT readiness

### Typical ISO/IEC 27001 Annex A controls to reference
- **A.5.29** Information security during disruption  
- **A.5.30** ICT readiness for business continuity  

---

## 5.1 BIA (Business Impact Analysis) — what to document

- Critical processes and services (what must be restored first)
- **RTO** (Recovery Time Objective) and **RPO** (Recovery Point Objective) per service
- Dependencies:
  - IdP (SSO)
  - DNS
  - Cloud region/provider
  - Third parties
  - Key staff
- Minimum resources needed (people, tools, access, runbooks, licenses)
- Security requirements during workaround modes
  - Don’t “turn off” security to recover

---

## 5.2 DR strategy patterns (technical)

- **Backups + restore**
  - Backup frequency, retention, immutability, restore testing

- **Redundancy**
  - Multi-AZ/region where justified by BIA

- **Failover**
  - Documented runbooks + regular testing

- **Alternative communications**
  - Out-of-band channels + contact trees

- **Evidence preservation**
  - Logging and forensic evidence handling remains possible during disruption

---

## 5.3 BIA summary template (excerpt)

| Process / Service | Owner | RTO | RPO | Key dependencies | Notes |
|---|---|---:|---:|---|---|
| Email & collaboration | IT Ops | 8h | 4h | IdP, DNS, SaaS provider | MFA mandatory even during disruption |
| Customer portal | Engineering | 2h | 15m | Cloud region, DB, WAF | Failover runbook tested quarterly |

---

## 5.4 Testing (what “good evidence” looks like)

- Backup restore test report:
  - date, scope, results, issues, corrective actions
- Tabletop exercise notes:
  - ransomware, region outage, IdP outage
- DR/failover drill evidence:
  - screenshots, timestamps, RTO/RPO achieved or missed
- Post-incident review and improvement actions tracked to closure

---

# 6. Evidence pack checklist (what auditors usually want)

Think like an auditor: **“Show me.”**

| Area | Artifacts / evidence |
|------|-----------------------|
| Risk | Methodology, risk register, SoA, treatment plan, acceptance records |
| Assets | Inventory with owners, classification scheme, acceptable use, lifecycle records |
| Access | Policies, IAM workflow, MFA enforcement, access reviews, logs |
| Continuity | BIA, RTO/RPO, DR plans/runbooks, tests, improvement actions |

---

# Appendix A — Risk register (blank template)

> Tip: keep IDs stable. Never delete risks; close them or mark as “retired” to preserve history.

| Risk ID | Scenario | Owner | L (1–5) | I (1–5) | Treatment (Mitigate/Accept/Transfer/Avoid) | Key controls / evidence |
|--------|----------|-------|--------:|--------:|-------------------------------------------|-------------------------|
| R-001  |          |       |         |         |                                           |                         |
| R-002  |          |       |         |         |                                           |                         |
| R-003  |          |       |         |         |                                           |                         |
| R-004  |          |       |         |         |                                           |                         |

---

# Appendix B — Statement of Applicability (SoA) excerpt

For each Annex A control, record whether it is applicable and your justification.

| Control | Applicable? | Justification | Implementation status | Evidence link(s) |
|--------|-------------|--------------|------------------------|------------------|
| A.5.9 Inventory of assets | Yes | Assets are in scope and must be protected | Implemented | Asset register export; review log |
| A.5.30 ICT readiness for BC | Yes | Critical services require defined RTO/RPO | In progress | BIA draft; backup test report |
| A.8.2 Privileged access rights | Yes | Admins exist for cloud and endpoints | Implemented | PAM policy; privileged group review |

---

# Appendix C — Asset register fields (recommended)

| Field group | Examples |
|---|---|
| Identifiers | Asset ID, hostname/account ID, serial number, tags |
| Ownership | Asset owner, system owner, data owner, custodian |
| Classification | Data classification, CIA rating (H/M/L) if you use it |
| Location | Physical location or cloud region/account/project |
| Lifecycle | Acquired date, end-of-life, decommission date, disposal method |
| Security controls | MFA, encryption, backups, logging, patch level, monitoring |
| Dependencies | Upstream/downstream systems, key suppliers, IdP, network zones |
| Continuity | RTO/RPO for the service the asset supports (if applicable) |

---

# Appendix D — DR test report (blank template)

Use this template to document evidence for **A.5.30** and **A.5.29**.

| Field | Value |
|------|-------|
| Test name |  |
| Date/time |  |
| Scope (systems, region, users) |  |
| Scenario |  |
| Objectives (RTO/RPO targets) |  |
| Steps performed |  |
| Results (achieved vs target) |  |
| Issues found |  |
| Corrective actions and owners |  |
| Sign-off |  |
