
# Ubuntu STIG & NIST 800-53 Hardening Project

This project demonstrates how to harden an Ubuntu 20.04 LTS server according to the **DISA STIG baseline** and map all actions to relevant **NIST SP 800-53 Rev. 5** controls. It simulates a DoD compliance workflow, including scanning, remediation, documentation, and continuous monitoring.

---

## Project Objectives

* Apply security configurations from the **Ubuntu STIG**
* Map STIG findings to **NIST 800-53 Rev. 5** control families
* Use **OpenSCAP** to scan for compliance
* Automate hardening with **Bash scripts**
* Generate **compliance documentation** (SSP, POA\&M, mapping tables)
* Simulate **continuous monitoring** and RMF Step 6

---

##  Tools & Technologies

* Ubuntu 20.04 LTS
* Bash scripting
* OpenSCAP
* SCAP Security Guide (Ubuntu STIG profile)
* Auditd, AIDE
* Cron (for scan automation)

---

## Structure

```bash
.
├── README.md
├── scripts/                # Hardening scripts
├── results/                # OpenSCAP scan reports (pre/post)
├── docs/                   # SSP, POA&M, NIST mapping
│   ├── SSP.md
│   ├── POAM.md
│   └── STIG-NIST-Mapping.md
```

---

## Quickstart

### 1. Run Initial OpenSCAP Scan

```bash
sudo apt install libopenscap8
sudo oscap xccdf eval \
  --profile xccdf_org.ssgproject.content_profile_stig \
  --results results/results.xml \
  --report results/ubuntu-stig-report.html \
  ssg-ubuntu2004-ds.xml
```

### 2. Apply Hardening Scripts

```bash
cd scripts/
sudo bash harden-ssh.sh
sudo bash audit-rules.sh
sudo bash enforce-password-policy.sh
```

### 3. Run Post-Remediation Scan

Same as step 1, save as `results/ubuntu-stig-postfix.html`

### 4. Review Compliance Docs

*

---

##  Key NIST Control Families Addressed

| STIG Area           | NIST 800-53 Controls    |
| ------------------- | ----------------------- |
| Account Management  | AC-2, IA-5, AC-7        |
| Audit & Logging     | AU-2, AU-3, AU-6, AU-12 |
| Configuration       | CM-6, CM-7, SI-2        |
| System Integrity    | SI-7, SI-4, SC-28       |
| Remote Access / SSH | AC-17, SC-8, SC-13      |

---

## Continuous Monitoring

* `cron` job runs OpenSCAP scan weekly
* Logs retained via `auditd`
* Future: forward logs to SIEM (e.g., Splunk or ELK)

---

## RMF Coverage

| RMF Step | Activity                              |
| -------- | ------------------------------------- |
| Step 3   | Implement STIG-aligned controls       |
| Step 4   | Assess with OpenSCAP scan             |
| Step 5   | Document residual risk in POA\&M      |
| Step 6   | Monitor via cron scans + log auditing |

---

## Documentation

* [System Security Plan (SSP)](docs/SSP.md)
* [Plan of Action & Milestones (POA\&M)](docs/POAM.md)
* [STIG to NIST Control Mapping](docs/STIG-NIST-Mapping.md)

---

## About

This project was created to demonstrate technical compliance, automation, and documentation skills relevant to **DoD SOC analyst** and **RMF-focused cybersecurity roles**.

---
