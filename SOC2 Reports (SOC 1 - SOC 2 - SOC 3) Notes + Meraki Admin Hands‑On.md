# SOC Reports (SOC 1 / SOC 2 / SOC 3) Notes + Meraki Hands‑On Appliance

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

Evaluates whether the same controls are **operating effectively** over a defined period (ex: 3–12 months).

* Example: “From *MM/DD/YYYY to MM/DD/YYYY*, alerts were reviewed, access was recertified, patches were applied on schedule, and exceptions were tracked.”

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

## Hands-on lab: Cisco Meraki Administrator (SOC 2‑aligned)

For the technical portion, I’m configuring a Meraki environment with a SOC 2 mindset: **reduce exposure, harden configs, and generate audit-ready evidence**.

Examples of Meraki controls that map well to SOC 2 (especially **Security / Availability / Confidentiality**):

* **Identity & admin security**

  * Enforce **MFA** and strong admin roles (least privilege)
  * Centralize authentication via **SSO** where possible
* **Network segmentation & traffic control**

  * VLANs / segmentation by function (user, server, guest, admin)
  * Layer 3/7 firewall rules, egress restrictions, deny-by-default patterns
* **Threat detection**

  * Enable **IDS/IPS** (where supported) and review events
  * Alerting for suspicious activity and config changes
* **Secure connectivity**

  * Site-to-site VPN, secure remote admin access, disable risky management paths
* **Monitoring & logging**

  * Export events to **Syslog/SIEM**, set retention expectations
  * Dashboard alerts for uplink changes, device health, VPN status
* **Operational hygiene**

  * Firmware lifecycle management (planned upgrades + rollback plan)
  * Config documentation + periodic reviews

Deliverables (portfolio-friendly):


## Note on confidentiality

Some details (customer names, IPs, internal diagrams, event logs) may be **redacted or excluded ** due to confidentiality agreements. This project is meant to demonstrate **how SOC 2 controls are applied and evidenced**, not to disclose sensitive operational data.
