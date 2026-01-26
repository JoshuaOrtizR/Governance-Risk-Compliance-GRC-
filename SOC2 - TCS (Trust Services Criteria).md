# SOC 2 Trust Services Criteria: Security (CC1–CC9) 

SOC 2 **Security** is the baseline criterion required in every SOC 2 report. In practice, Security is assessed using the **Common Criteria (CC1–CC9)**, which cover governance, risk, operations, and technical control execution.

Below is a brief, technical breakdown of each CC area and what I typically implement/collect as evidence as a cybersecurity engineer working in **compliance, risk, and governance**.

---

## TSC Security Common Criteria (CC1–CC9)

| CC      | Domain                                 | What it’s proving                                                     | Typical technical controls                                                                              | Common audit evidence                                                                             |
| ------- | -------------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **CC1** | **Control Environment**                | Leadership sets expectations, roles, and accountability for security  | Security org structure, defined control ownership, security awareness, policy governance                | Org chart, security policies, training completion, RACI, security committee minutes               |
| **CC2** | **Communication & Information**        | Security requirements and system info are communicated and documented | System documentation, data flow diagrams, incident comms plan, security standards/baselines             | System description, diagrams, policy distribution records, onboarding/offboarding procedures      |
| **CC3** | **Risk Assessment**                    | Risks are identified, analyzed, and treated                           | Risk register, threat modeling, risk scoring, risk acceptance workflow                                  | Risk assessment methodology, risk register, risk treatment plans, approvals for exceptions        |
| **CC4** | **Monitoring Activities**              | Controls are monitored and validated over time                        | SIEM monitoring, alerting, detection use-cases, control testing cadence, KPI/KRIs                       | SIEM dashboards, alert tickets, weekly/monthly review notes, internal control test results        |
| **CC5** | **Control Activities**                 | Security controls are designed and executed to meet objectives        | Network segmentation, secure configs, encryption, vuln mgmt, backups, endpoint controls                 | Config screenshots/exports, scan reports, backup logs, standard build docs, control matrix        |
| **CC6** | **Identity & Access Management (IAM)** | Access is authorized, least privilege, and reviewed                   | SSO, MFA, RBAC, privileged access controls, joiner-mover-leaver (JML), periodic access reviews          | IdP settings, access review sign-offs, JML tickets, admin role assignments, auth logs             |
| **CC7** | **System Operations**                  | Systems are operated securely day-to-day                              | Patching, incident response, EDR, logging, capacity/uptime monitoring, backup restore testing           | Patch reports, IR tickets/postmortems, operational runbooks, uptime/alerts, restore test evidence |
| **CC8** | **Change Management**                  | Changes are controlled, reviewed, and tracked                         | Change tickets, approvals, CI/CD controls, code review, segregation of duties, emergency change process | Change records, PR approvals, pipeline logs, release notes, rollback plans, CAB approvals         |
| **CC9** | **Risk Mitigation**                    | Risks are mitigated via plans, vendors, resilience, and remediation   | Vendor risk management, DR/BCP, remediation tracking, security exception handling                       | Vendor reviews, BCP/DR test results, POA&M/remediation tracker, risk acceptance records           |

---

## Preparing for SOC 2 Compliance (Readiness → Audit)

### 1) Gap analysis & readiness assessment

**Objective:** Compare current state to CC1–CC9 requirements and define a remediation plan.

**Deliverables (practical):**

* **Control Matrix** (CC → control → owner → evidence → frequency)
* Evidence inventory (what exists vs missing)
* Remediation backlog (tickets with priority + due dates)

---

### 2) Building a compliance team (GRC + technical ownership)

**Objective:** Assign clear ownership so evidence collection doesn’t break during audits.

**What “good” looks like:**

* Control Owner (accountable) vs Evidence Owner (operational)
* RACI across Security, IT Ops, Engineering, HR, Legal, Vendor Mgmt
* Defined escalation path for exceptions and overdue controls

---

### 3) Defining system boundaries (scope)

**Objective:** Clearly define what is **in-scope** for the SOC 2 report.

**Include:**

* In-scope products/services, environments (prod/stage), regions
* Data types + data flows (PII, credentials, logs, footage, etc.)
* Subservice orgs / third parties (e.g., cloud providers, MSSPs)
* Shared responsibility + relevant **CUECs** (customer controls if applicable)

**Deliverables:**

* System description + boundary statement
* Network/data flow diagrams (high level, portfolio-safe)

---

### 4) Documenting policies & procedures (make controls repeatable)

**Objective:** Convert “tribal knowledge” into enforceable, auditable processes.

**Minimum policy set (common SOC 2):**

* Access control + MFA/SSO
* Logging/monitoring
* Vulnerability/patch management
* Change management
* Incident response
* Vendor risk management
* Backup/DR/BCP

**Tip:** Procedures/runbooks matter as much as policies (how the control is executed).

---

### 5) Risk assessment methodology (make risk decisions defensible)

**Objective:** Establish a consistent way to measure and treat risk.

**Core components:**

* Likelihood/impact scoring model
* Risk treatment options (accept/mitigate/transfer/avoid)
* Review frequency (e.g., quarterly + major-change triggers)
* Exception workflow (approval + expiration + compensating controls)

**Deliverables:**

* Risk methodology doc
* Risk register tied to control selection and remediation tickets

---

## Evidence Hygiene for Type I vs Type II

* **Type I:** prove the control is **designed/implemented** (point-in-time screenshots/config exports)
* **Type II:** prove the control **operates consistently** (tickets, logs, reviews, approvals over time)

<div align="center">
  
## Joshua Ortiz  
**Governance, Risk & Compliance Consultant**

</div>
