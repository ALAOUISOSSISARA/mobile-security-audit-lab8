# LAB 8 - Mobile Application Security Analysis

## Overview

This repository contains the complete deliverables for LAB 8 of the Mobile Application Security course. The objective of this lab is to perform a defensive security audit of a mobile application using open-source intelligence tools, correlate findings with OWASP standards, and produce a structured analysis report.

**Analyst:** ALAOUI SOSSI SARA  
**Date:** 2026-05-04  
**Course:** Securite des applications mobiles  
**Platform:** MLIAEdu  

---

## Target Application

| Field | Value |
|-------|-------|
| Application | UnCrackable Level 1 |
| Package | owasp.mstg.uncrackable1 |
| Version | 1.0 |
| Source | OWASP Mobile Application Security Testing Guide (MASTG) |
| SHA-256 | 1DA8BF57D266109F9A07C01BF7111A1975CE01F190B9D914BCD3AE3DBEF96F21 |
| Type | Pedagogical APK - intentionally vulnerable |

<img width="1267" height="683" alt="image" src="https://github.com/user-attachments/assets/8ecd4fdc-d1cd-4a10-8198-bfb18dc721b1" />


---

## Legal and Ethical Framework

This analysis was conducted strictly within a legal and defensive framework.

- Target: OWASP MASTG public pedagogical APK
- Authorization: Open-source application designed for security training
- Scope: Static analysis only, no exploitation, no intrusive testing
- All sensitive values discovered are masked in this repository

---

## Tools Used

| Tool | Version | Purpose | Status |
|------|---------|---------|--------|
| BeVigil (CloudSEK) | Web platform | External OSINT and static analysis | Available |
| Yaazhini | 1.x | Deep static APK analysis | Unavailable - domain expired (May 2026) |

> Note: Yaazhini (yaazhini.com) was unavailable at the time of analysis due to an expired domain. Tasks 5 and 6 were documented accordingly. The BeVigil analysis covers equivalent static analysis capabilities.

---

## Repository Structure

```
lab-mobile-security/
│
├── 00-scope/
│   ├── scope.md                    # Analysis perimeter and authorization
│   └── UnCrackable-Level1.apk      # Target APK (pedagogical)
│
├── 01-bevigil/
│   ├── bevigil_notes.md            # Structured BeVigil analysis notes
│   ├── vulnerabilities.txt         # Detected vulnerabilities
│   ├── strings.txt                 # Hardcoded strings and secrets
│   ├── assets.txt                  # Exposed file paths and assets
│   ├── apkid.txt                   # Compiler and anti-analysis detection
│   ├── appdata.txt                 # App components and permissions
│   └── trackers_libraries.txt      # Trackers and third-party libraries
│
├── 02-yaazhini/
│   ├── yaazhini_notes.md           # Analysis notes (based on BeVigil data)
│   └── note_indisponible.txt       # Tool unavailability documentation
│
├── 03-triage/
│   ├── triage.csv                  # Normalized findings (10 entries)
│   └── owasp_mapping.md            # OWASP MASVS correlation (6 mappings)
│
├── 04-report/
│   └── rapport_final.md            # Final security analysis report
│
├── analyse_info.txt                # Analysis metadata and traceability
├── commands.log                    # Command history log
├── checklist_fin.md                # End-of-analysis signed checklist
└── README.md                       # This file
```

---

## Key Findings Summary

| ID | Finding | Severity | OWASP Reference |
|----|---------|----------|----------------|
| FIND-001 | Hardcoded AES key in source code | High | MASVS-CRYPTO-1 |
| FIND-002 | Weak AES-ECB encryption algorithm (CWE-327) | High | MASVS-CRYPTO-1 |
| FIND-003 | Bypassable root detection (CWE-200) | Medium | MASVS-RESILIENCE-1 |
| FIND-004 | Super-user privileges requested (CWE-250) | Medium | MASVS-PLATFORM-1 |
| FIND-005 | Bypassable anti-VM check (Build.TAGS only) | Low | MASVS-RESILIENCE-4 |
| FIND-006 | No code obfuscation (dx compiler) | Low | MASVS-CODE-1 |
| FIND-007 | Single exported Activity | Low | MASVS-PLATFORM-3 |
| FIND-008 | No Android permissions declared | Info | MASVS-PLATFORM-1 |
| FIND-009 | No advertising trackers | Info | MASVS-STORAGE-4 |
| FIND-010 | No third-party libraries | Info | MASVS-CODE-3 |

**BeVigil Security Rating:** 8.3 / 10 (Good)  
> This score does not reflect the actual risk level. The hardcoded cryptographic key represents a critical vulnerability that static scoring tools may underweight in the context of a minimal pedagogical application.
<img width="1552" height="271" alt="image" src="https://github.com/user-attachments/assets/cc778da6-251f-4e84-a3ce-a8ac25aec158" />
<img width="1920" height="795" alt="image" src="https://github.com/user-attachments/assets/11130582-1c26-4eb4-8c7f-fdea02532941" />
<img width="1920" height="386" alt="image" src="https://github.com/user-attachments/assets/bd960271-3ac4-41f4-ae8e-56fd757b59e3" />


---

## OWASP MASVS Correlation

| Category | Description | Findings |
|----------|-------------|---------|
| MASVS-CRYPTO | Cryptography | FIND-001, FIND-002 |
| MASVS-RESILIENCE | Anti-tampering and anti-analysis | FIND-003, FIND-005 |
| MASVS-PLATFORM | Platform interaction | FIND-004, FIND-007, FIND-008 |
| MASVS-CODE | Code quality | FIND-006, FIND-010 |
| MASVS-STORAGE | Data storage | FIND-009 |

---

## Priority Recommendations

1. Remove all cryptographic keys from source code and store them using the Android Keystore system.
2. Replace AES-ECB with AES-GCM using a random initialization vector for all encryption operations.
3. Implement multi-layered root detection using the Play Integrity API instead of relying on a single file path check.

---

## Methodology

The analysis followed a structured 10-step workflow:

1. Scope definition and ethical framework documentation
2. Workspace preparation and traceability setup
3. Authorized artifact preparation and hash verification
4. BeVigil platform analysis - setup and familiarization
5. BeVigil data collection - endpoints, strings, assets, technologies
6. Yaazhini analysis - documented as unavailable
7. Yaazhini data collection - documented as unavailable
8. Findings normalization and deduplication
9. OWASP MASVS correlation
10. Report writing and workspace cleanup

---

## References

- OWASP Mobile Application Security Testing Guide (MASTG): https://github.com/OWASP/owasp-mastg
- OWASP Mobile Application Security Verification Standard (MASVS): https://github.com/OWASP/owasp-masvs
- BeVigil by CloudSEK: https://bevigil.com
- UnCrackable Level 1 (target APK): https://github.com/OWASP/owasp-mastg/blob/master/Crackmes/Android/Level_01/UnCrackable-Level1.apk

---

## Disclaimer

This analysis was performed exclusively for educational purposes within the scope of a supervised security course. The target application is an intentionally vulnerable open-source application provided by OWASP for training purposes. No exploitation techniques were applied and no systems were harmed during this analysis.
