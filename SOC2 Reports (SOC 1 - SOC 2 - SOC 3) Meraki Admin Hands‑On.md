# SOC Reports (SOC 1 / SOC 2 / SOC 3) + Meraki Hands‑On Appliance

## What “SOC” means
**SOC (System and Organization Controls)** refers to assurance reports issued under **AICPA** guidance that evaluate how an organization designs and operates controls. The goal is to reduce organizational exposure by proving controls are **designed well** and (depending on report type) **operate effectively over time**.

For cybersecurity work, the most relevant one is **SOC 2**, which maps controls to the **Trust Services Criteria (TSC)**:

* **Security** (required in every SOC 2)
* **Availability**
* **Confidentiality**
* **Processing Integrity**
* **Privacy**

## SOC categories (what they’re used for)

* **SOC 1**: Controls relevant to **financial reporting (ICFR)**. Common for payroll processors, billing platforms, and vendors impacting a customer’s financial statements.
* **SOC 2**: Controls aligned to the **Trust Services Criteria** (security/availability/confidentiality/etc.). Common for SaaS, cloud, MSPs, and tech providers.
* **SOC 3**: A **public, high-level summary** of SOC 2 (less detail, used for marketing/website trust pages).

## SOC 2 report types (Type I vs Type II)

### SOC 2 Type I (point-in-time)

Evaluates whether controls are **designed appropriately** and implemented as of a **specific date**.

* Example: “On *MM/DD/YYYY*, MFA was enforced for admins and firewall rules were configured per standard.”

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

 **Note:**
Some details (customer names, IPs, internal diagrams, event logs) may be **redacted/excluded** due to confidentiality agreements. This is meant to demonstrate 

**how SOC 2 controls are applied and evidenced**, not to disclose sensitive operational data.

## Cisco Meraki Administrator (SOC 2‑aligned)

# SOC 2 Notes + Cisco Meraki Lab (Evidence-Based Controls)

> I’m learning cybersecurity and GRC. This repo section documents **how SOC 2 controls are applied and evidenced** using Cisco Meraki configuration and screenshots—**without disclosing sensitive operational data**.

---

## What SOC Means (System and Organization Controls)

**SOC (System and Organization Controls)** is an assurance reporting framework (AICPA) used to evaluate whether an organization has **controls designed and operating** to protect systems and data.

For cybersecurity work, SOC reports commonly align to the **Trust Services Criteria (TSC)**:

* **Security** *(required for all SOC 2 reports)*
* **Availability**
* **Confidentiality**
* **Processing Integrity**
* **Privacy**

SOC reports help reduce organizational exposure by proving controls exist, are implemented correctly, and (for Type II) are consistently followed.

---
## SOC Categories (SOC 1 / SOC 2 / SOC 3)

* **SOC 1**: Controls relevant to **financial reporting** (ICFR). Used when a vendor’s system impacts a customer’s financial statements.
* **SOC 2**: Controls aligned to **Trust Services Criteria** (Security, Availability, Confidentiality, etc.). Common for SaaS, cloud, MSPs, and IT service providers.
* **SOC 3**: A **public, high-level** version of SOC 2 (less detail, typically used for marketing/trust pages).

---

## SOC 2 Report Types (Type I vs Type II)

* **SOC 2 Type I (Point-in-time)**
  Verifies controls are **designed appropriately** and implemented as of a specific date.

* **SOC 2 Type II (Operating effectiveness)**
  Verifies those controls operate **consistently over a period of time** (e.g., 3–12 months), including monitoring, reviews, and evidence retention.

---

## Project Scope: Cisco Meraki Administrator (SOC 2‑Aligned)

I’m configuring a Meraki environment with a SOC 2 mindset:

* **Reduce exposure**
* **Harden configurations**
* **Generate audit-ready evidence** (screenshots, logs, settings exports, and documented reviews)

### Screenshot location

Place the screenshots in this repo path:

```
/assets/meraki/
```

These image links assume the following filenames (spaces included). GitHub renders them correctly because spaces are URL-encoded.

---

# Meraki Evidence Walkthrough

## Policy Objects (Standardized Rule Targets)

![Create policy object - VPN\_Gateway](./assets/meraki/Policy%20Object.jpeg)

**What I did**

* Created a **Policy Object** named `VPN_Gateway` pointing to a defined IP (example shown).
* This object becomes a reusable named target for firewall rules, group policies, and ACLs.

**Technical value**

* Prevents rule sprawl and reduces misconfig risk (no repeated manual IP entry).
* Makes rules more readable and supports standardized change control.

**SOC 2 mapping**

* **Security**: controlled access paths + reduced admin error.
* **Change management**: named objects are easier to review and approve.

**Evidence**

* **Type I**: screenshot of the object definition (name + IP/FQDN/CIDR).
* **Type II**: change log + periodic review of policy objects (ownership + justification).

---

##  Adaptive Policy ACL (Segmentation + Least Privilege)

![Add Adaptive Policy ACL](./assets/meraki/Adaptive%20policy%20ACL.jpeg)

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

**Evidence**

* **Type I**: screenshot of ACL creation and rule intent.
* **Type II**: documented rule review cadence + proof of ongoing monitoring/log review.

---

## Camera & Sensor Role Management (RBAC for Sensitive Data)

![Camera and sensor role management](./assets/meraki/Camera%20and%20Roles.jpeg)

**What I did**

* Reviewed/configured **role-based access** for camera footage access levels (examples shown):

  * View + export footage
  * View footage
  * View live only

**Technical value**

* RBAC enforces **least privilege** for high-risk data (footage exports are higher risk than view-only).
* Supports access reviews and reduces insider-risk exposure.

**SOC 2 mapping**

* **Confidentiality / Privacy**: restrict sensitive data access based on role.
* **Security**: enforce authorization boundaries.

**Evidence**

* **Type I**: screenshot showing role permissions and available options.
* **Type II**: recurring access review evidence (export who has access, approvals, and removals).

---

## Authentication Evidence (SSO / MFA Login Attempts)

![Dashboard login attempts](./assets/meraki/logs.jpeg)

**What I did**

* Validated **login attempt logs** for:

  * Authentication type (e.g., **SAML** / SSO)
  * **Two-Factor Auth** successes and failures
  * Source metadata (IP/geo) — redacted in public screenshots

**Technical value**

* Login telemetry supports detection of:

  * brute-force attempts
  * MFA fatigue patterns
  * suspicious geo activity
* Confirms centralized authentication design (SSO) and enforcement (MFA).

**SOC 2 mapping**

* **Security**: logical access controls + authentication monitoring.
* **Availability**: early detection helps prevent account compromise leading to outages.

**Evidence**

* **Type I**: screenshot showing SSO/MFA activity records.
* **Type II**: documented log review cadence + ticket/incident record for anomalies.

---

## Threat Protection (AMP + IDS/IPS + Optional Integrations)

![Threat protection settings](./assets/meraki/Threat%20Protectiton.jpeg)

**What I did**

* Enabled **Advanced Malware Protection (AMP)**.
* Set **IDS ruleset** to a stronger security posture (example shown: `Security`).
* Kept allow lists empty by default; exceptions require justification and approval.
* Noted optional integrations shown in UI (Umbrella protection, XDR enablement).

**Technical value**

* AMP reduces malware exposure via reputation/analysis-based protections.
* IDS/IPS adds network-layer detection/prevention for known threat patterns.
* Exceptions (allow lists) are treated as controlled changes with expiration and review.

**SOC 2 mapping**

* **Security**: malware prevention + intrusion detection.
* **Change management**: documented exceptions and approvals.

**Evidence**

* **Type I**: screenshot of AMP enabled + IDS ruleset selected.
* **Type II**: event review records + exception register (what, why, who approved, when reviewed).

---

## Content Filtering (Block High-Risk Categories)

![Content filtering configuration](./assets/meraki/Content%20Filtering.jpeg)

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

**Evidence**

* **Type I**: screenshot of category and threat settings.
* **Type II**: periodic review of exceptions and blocked event trends.

---

## Alerts & Availability Monitoring (Operational Signal + Response)

![Alerts dashboard](./assets/meraki/Alerts.jpeg)

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

**Evidence**

* **Type I**: screenshot showing alerts dashboard and active alerts.
* **Type II**: ticketing/incident workflow evidence (alert → triage → fix → closure).

---

# Control-to-Evidence Map (SOC 2 Mindset)

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
# Joshua Ortiz  
**Governance, Risk & Compliance Consultant**
</div>




