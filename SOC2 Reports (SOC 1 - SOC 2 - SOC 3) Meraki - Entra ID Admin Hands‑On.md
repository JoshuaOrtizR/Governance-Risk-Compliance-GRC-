## SOC Reports (SOC 1 / SOC 2 / SOC 3) + Meraki - Entra ID / Hands‑On Appliance

**SOC (System and Organization Controls)** refers to assurance reports issued under **AICPA** guidance that evaluate how an organization designs and operates controls. The goal is to reduce organizational exposure by proving controls are **designed well** and (depending on report type) **operate effectively over time**.

For cybersecurity work, the most relevant one is **SOC 2**, which maps controls to the **Trust Services Criteria (TSC)**:

* **Security** (required in every SOC 2)
* **Availability**
* **Confidentiality**
* **Processing Integrity**
* **Privacy**

**SOC categories (what they’re used for)**

* **SOC 1**: Controls relevant to **financial reporting (ICFR)**. Common for payroll processors, billing platforms, and vendors impacting a customer’s financial statements.
* **SOC 2**: Controls aligned to the **Trust Services Criteria** (security/availability/confidentiality/etc.). Common for SaaS, cloud, MSPs, and tech providers.
* **SOC 3**: A **public, high-level summary** of SOC 2 (less detail, used for marketing/website trust pages).

## SOC 2 report types (Type I vs Type II)

### SOC 2 Type I (point-in-time)

Evaluates whether controls are **designed appropriately** and implemented as of a **specific date**.

* Example: “On MM/DD/YYYY, MFA was enforced for admins and firewall rules were configured per standard.”

### SOC 2 Type II (over a period of time)

Evaluates whether the same controls are **operating effectively** over a defined period (3–12 months).

* Example:From MM/DD/YYYY to MM/DD/YYYY, alerts were reviewed, access was recertified, patches were applied on schedule, and exceptions were tracked.

## What a GRC / SOC 2 auditor usually validates (My Takepoints)

In practice, you prove controls with **evidence**. Typical items include:

* **Access control**: SSO/MFA enforcement, RBAC, joiner-mover-leaver process, access reviews, privileged access management
* **Logging & monitoring**: SIEM/syslog exports, alert rules, incident tickets, escalation procedures, time sync (NTP), log retention
* **Change management**: change tickets, approvals, implementation plans, rollback plans, post-change validation
* **Vulnerability & patch management**: scan results, remediation SLAs, patch schedules, exception tracking
* **Network security**: segmentation, firewall rules, IDS/IPS, secure remote access, configuration standards
* **Policies + procedures**: security policy, incident response plan, risk assessment, vendor risk reviews
* **Ongoing governance**: metrics, reviews, management sign-off, audit trails

A lot of SOC work is: **control → evidence → traceability** (can you prove what happened, when, and who approved it?).

### Note:
**Some details (Client's data, IPs, internal diagrams, event logs) may be redacted/excluded due to confidentiality agreements. This is meant to demonstrate how SOC 2 controls are applied and evidenced, not to disclose sensitive operational data.**

## Cisco Meraki / Azure Entra ID (Evidence-Based Controls)

I’m configuring a Meraki/ Entra ID environment with a SOC 2 mindset:

* **Reduce exposure**
* **Harden configurations**
* **Generate audit-ready evidence** (screenshots, logs, settings exports, setting up controls, and documented reviews)

## Policy Objects (Standardized Rule Targets)

![Image](https://github.com/user-attachments/assets/d022c1a0-cf67-4502-ac8c-0107f2d0d803)

![Image](https://github.com/user-attachments/assets/9ca42db8-d16d-4bbc-a159-1446ad1477eb)

**What I did**
* Created a **Policy Object** named `VPN_Gateway` pointing to a defined IP.
* This object becomes a reusable named target for firewall rules, group policies, and ACLs.

**Technical value**
* Prevents rule sprawl and reduces misconfig risk (no repeated manual IP entry).
* Makes rules more readable and supports standardized change control.

**SOC 2 mapping**
* **Security**: controlled access paths + reduced admin error.
* **Change management**: named objects are easier to review and approve.

---

##  Adaptive Policy ACL (Segmentation + Least Privilege)

![Image](https://github.com/user-attachments/assets/8097a8d5-0c0b-4298-acfc-ab2730b487d0)

![Image](https://github.com/user-attachments/assets/ce863ef9-b6d2-4cdf-acce-ad288950d76d)

**What I did**
* Created an **Adaptive Policy ACL** named `VPN_Gateway`.
* Added a description documenting intent: *only approved traffic to the VPN gateway*.
* Selected **IPv4** scope (IPv6 should be documented separately if used).

**Technical value**

* Supports segmentation and controlled east-west traffic flows.
* Enables a “**default deny** + explicit allow” posture (depending on design and enforcement points).
* Clear naming + descriptions improve audit traceability and operational clarity.

**SOC 2 mapping**

* **Security**: least privilege network access.
* **Confidentiality**: reduces unauthorized access to sensitive endpoints.

---

## Camera & Sensor Role Management (RBAC for Sensitive Data)

![Image](https://github.com/user-attachments/assets/866783d0-d10f-4030-a073-c97ad07c5ac6)

![Image](https://github.com/user-attachments/assets/a8708cfc-13ec-407e-8cc9-9bcd165fde04)

**What I did**

* Reviewed/configured **role-based access** for camera footage access levels:

  * View + export footage
  * View footage
  * View live only

**Technical value**

* RBAC enforces **least privilege** for high-risk data (footage exports are higher risk than view-only).
* Supports access reviews and reduces insider-risk exposure.

**SOC 2 mapping**

* **Confidentiality / Privacy**: restrict sensitive data access based on role.
* **Security**: enforce authorization boundaries.

## Authentication Evidence (SSO / MFA Login Attempts)

![Image](https://github.com/user-attachments/assets/399b0d03-4da2-4fd2-bf5f-c3b10bd8194d)

![Image](https://github.com/user-attachments/assets/faabdf52-91f5-470f-b671-64be761640d8)

**What I did**

* Validated **login attempt logs** for:

  * Authentication type (e.g., **SAML** / SSO)
  * **Two-Factor Auth** successes and failures
  * Source metadata (IP/geo) 

**Technical value**

* Login telemetry supports detection of:

  * brute-force attempts
  * MFA fatigue patterns
  * suspicious geo activity
* Confirms centralized authentication design (SSO) and enforcement (MFA).

**SOC 2 mapping**

* **Security**: logical access controls + authentication monitoring.
* **Availability**: early detection helps prevent account compromise leading to outages.

---

## Threat Protection (AMP + IDS/IPS + Optional Integrations)

![Image](https://github.com/user-attachments/assets/5815539c-4267-44d9-afab-3870f1c17f75)

![Image](https://github.com/user-attachments/assets/08b67386-b026-4467-975e-e5723b15cdc7)

**What I did**

* Enabled **Advanced Malware Protection (AMP)**.
* Set **IDS ruleset** to a stronger security posture (`Security`).
* Kept allow lists empty by default; exceptions require justification and approval.
* Noted optional integrations shown in UI (Umbrella protection, XDR enablement).

**Technical value**

* AMP reduces malware exposure via reputation/analysis-based protections.
* IDS/IPS adds network-layer detection/prevention for known threat patterns.
* Exceptions (allow lists) are treated as controlled changes with expiration and review.

**SOC 2 mapping**

* **Security**: malware prevention + intrusion detection.
* **Change management**: documented exceptions and approvals.

---

## Content Filtering (Block High-Risk Categories)

![Image](https://github.com/user-attachments/assets/bb216e97-1cef-4b82-bfa3-4af6966209be)

![Image](https://github.com/user-attachments/assets/45478de7-0c96-4fee-970a-6031da075b88)

**What I did**

* Configured category blocking to reduce exposure to:

  * **Threat categories** (e.g., malware, spyware/adware, phishing, open proxies)
  * **Risk categories** aligned to acceptable-use policy needs (example shown)

**Technical value**

* Blocking **phishing/malware** reduces credential theft and drive-by downloads.
* Blocking **open proxies** reduces control bypass and potential data exfil paths.
* URL allow/block lists exist for business exceptions (documented + approved).

**SOC 2 mapping**

* **Security**: preventative controls to reduce web-based threats.
* **Confidentiality**: reduces likelihood of credential compromise and data loss.

---

## Alerts & Availability Monitoring (Operational Signal + Response)

![Image](https://github.com/user-attachments/assets/df12e7a0-017c-429d-9988-7f648d254f5f)

![Image](https://github.com/user-attachments/assets/dd698f2c-958d-4b4f-969c-4e8704a6482f)

**What I did**

* Reviewed alert visibility and health monitoring signals, such as:

  * **Unreachable device** (availability risk)
  * **Port VLAN mismatch** (segmentation/integrity risk)
  * **CRC errors** (physical layer issues → packet loss/instability)

**Technical value**

* Alerts enable faster detection and response (reduced downtime).
* VLAN mismatches can cause traffic to land in the wrong segment—important for both security and availability.
* CRC errors often indicate cabling/transceiver issues and should trigger corrective action.

**SOC 2 mapping**

* **Availability**: monitoring + response improves uptime and resilience.
* **Security**: segmentation issues are detectable and correctable.


## Control-to-Evidence Map (SOC 2 Mindset)

| Control Area                   | Meraki Feature(s)      | Evidence I Capture                              |
| ------------------------------ | ---------------------- | ----------------------------------------------- |
| Standardized rule targets      | Policy Objects         | Object screenshots + object inventory review    |
| Segmentation / least privilege | Adaptive Policy ACL    | ACL screenshots + rule review notes             |
| Sensitive data authorization   | Camera role management | Role config screenshots + access review records |
| Strong authentication          | SSO (SAML) + MFA logs  | Login attempts screenshot + review cadence      |
| Malware & intrusion protection | AMP + IDS ruleset      | Threat protection screenshot + event review     |
| Web threat reduction           | Content filtering      | Policy screenshot + exception approvals         |
| Monitoring & availability      | Alerts dashboard       | Alerts screenshot + ticket/incident proof       |

---
<div align="center">
  
## Joshua Ortiz  
**Governance, Risk & Compliance Consultant**

</div>




