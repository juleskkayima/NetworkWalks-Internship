# 🔐 NetworkWalks — Mediroza General Hospital Penetration Test

![NetworkWalks](https://img.shields.io/badge/NetworkWalks-Week%204-blue)
![Cybersecurity](https://img.shields.io/badge/Focus-Penetration%20Testing-red)
![Testing](https://img.shields.io/badge/Type-Black--Box%20Pentest-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Environment](https://img.shields.io/badge/Environment-Authorized%20Lab-purple)

> **NetworkWalks Cybersecurity Training — Batch B083 | Week 4**

A controlled black-box penetration-testing exercise conducted against the simulated **Mediroza General Hospital** web infrastructure.

---

## ⚠️ Disclaimer

This project was conducted in a **controlled educational environment** with explicit authorization for security testing.

The techniques discussed in this repository must **never be applied to systems, websites, networks, accounts, or applications without explicit written permission from the owner**.

No real patient information or unauthorized third-party systems were targeted.

---

# 📋 Project Overview

| Field             | Details                                        |
| ----------------- | ---------------------------------------------- |
| **Project**       | Penetration Testing & Vulnerability Assessment |
| **Client**        | Mediroza General Hospital                      |
| **Target**        | `https://medirozahospital.com`                 |
| **Testing Type**  | Black-box penetration test                     |
| **Duration**      | 5 Days                                         |
| **Batch**         | B083                                           |
| **Week**          | 4                                              |
| **Scope**         | Target web infrastructure                      |
| **Authorization** | Granted                                        |
| **Environment**   | Controlled educational environment             |

---

# 🎯 Objectives

The main objective of this engagement was to assess the security of the simulated hospital web application from an external attacker's perspective.

The assessment focused on:

* Reconnaissance
* Web application security
* Authentication weaknesses
* Input validation
* Access-control weaknesses
* Sensitive information exposure
* File security
* Metadata analysis
* Backup exposure
* Database information exposure
* Vulnerability documentation
* Risk assessment
* Remediation recommendations

---

# 🗺️ Engagement Scope

The assessment was limited to the authorized target:

```text
https://medirozahospital.com
```

### Included

* Publicly accessible web resources
* Authorized patient portal
* Authorized files exposed through the application
* Authorized server directories
* Information discovered through the assessment

### Out of Scope

The following activities were explicitly excluded:

* Social engineering
* Denial-of-service testing
* Attacks against unrelated systems
* Testing outside the target domain
* Attacks against real-world infrastructure
* Unauthorized access to third-party systems

---

# 🧪 Testing Methodology

The assessment followed a structured penetration-testing workflow:

```text
                ┌─────────────────┐
                │  Reconnaissance │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   Enumeration   │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Authentication  │
                │    Testing      │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Vulnerability   │
                │ Identification  │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │   Controlled    │
                │ Exploitation    │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Data Exposure   │
                │   Analysis      │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Reporting &     │
                │ Remediation     │
                └─────────────────┘
```

---

# 🏁 Project Milestones

The engagement was divided into four major milestones.

## M1 — Initial Access

### Objective

Identify weaknesses in the web application that could allow access to the restricted patient area.

### Activities

The assessment included:

* Initial reconnaissance
* Identification of publicly referenced directories
* Analysis of the patient portal
* Authentication behaviour testing
* Username enumeration testing
* Input validation testing
* SQL injection assessment
* Controlled verification of the identified authentication weakness
* Retrieval of the three authorized test PDF reports

### Result

The assessment identified multiple weaknesses in the authentication mechanism.

The application disclosed whether a username existed through different authentication error messages.

Further testing identified an SQL injection vulnerability in the login functionality.

The vulnerability allowed the authentication mechanism to be bypassed within the controlled environment.

### Evidence Obtained

Three patient-report PDF files were accessible through the compromised test portal:

```text
patient_report_1.pdf
patient_report_2.pdf
patient_report_3.pdf
```

---

# 🔓 M2 — Protected File Assessment

## Objective

Assess the security of the three retrieved PDF reports.

The assessment determined that the files were protected using password-based PDF encryption.

### Activities

The assessment included:

* Identification of PDF encryption
* Extraction of information required for authorized password recovery
* Password-strength assessment
* Testing against approved wordlists
* Comparison of results between different password dictionaries
* Recovery of the protected files in the authorized environment

### Findings

Two of the files used weak passwords that were recoverable using a common-password list.

The third file required a larger authorized password dictionary before its password could be recovered.

This demonstrated that relying on weak or predictable passwords provides limited protection for sensitive documents.

### Security Lesson

File encryption is only as strong as the password protecting the file.

Sensitive documents should use:

* Strong unique passwords
* Appropriate key management
* Secure storage
* Access controls
* Proper document lifecycle management

---

# 🔎 M3 — Deep Reconnaissance & Data Exposure

## Objective

Investigate information discovered during the previous milestones and determine whether additional sensitive information was exposed.

### Metadata Analysis

The third PDF contained metadata that provided an important clue about the server environment.

The metadata included:

* Document author information
* A comment referencing an old database backup
* A reference to a legacy server directory

This demonstrated the importance of examining not only the visible contents of files but also their metadata.

---

## 📂 Exposed Backup Directory

Further investigation identified an old server directory associated with the application.

Directory listing was enabled, exposing an old database backup file.

```text
mediroza_db_backup_2019.sql
```

The presence of a database backup inside a publicly accessible web directory represented a serious information-disclosure issue.

---

# 🗄️ Database Exposure

The exposed database backup contained information belonging to different database tables.

The assessment focused on identifying the security impact rather than reproducing sensitive information in this repository.

The exposed information included:

### Staff Information

* Employee names
* Job titles
* Departments
* Monthly salary information

### Shareholder Information

* Shareholder names
* Share ownership percentages
* Share classes

This demonstrated how a single exposed backup can result in significant secondary information disclosure.

---

# 🔗 Attack Chain

One of the key lessons from this assessment was that vulnerabilities can form a chain.

The overall sequence was:

```text
Public Reconnaissance
        │
        ▼
Exposed Application Paths
        │
        ▼
Patient Login Portal
        │
        ▼
Username Enumeration
        │
        ▼
SQL Injection
        │
        ▼
Authentication Bypass
        │
        ▼
Patient PDF Reports
        │
        ▼
Weak File Passwords
        │
        ▼
PDF Metadata
        │
        ▼
Legacy Server Directory
        │
        ▼
Exposed Database Backup
        │
        ▼
Sensitive Staff & Shareholder Data
```

This demonstrates why penetration testing should not focus only on isolated vulnerabilities.

A low- or medium-severity information leak can sometimes provide information that enables discovery of a much more serious exposure.

---

# 🚨 Vulnerability Summary

| # | Vulnerability                                                    | Location        | Risk     |
| - | ---------------------------------------------------------------- | --------------- | -------- |
| 1 | Username enumeration                                             | Patient login   | Medium   |
| 2 | SQL injection in authentication                                  | Patient login   | Critical |
| 3 | Sensitive patient reports accessible after authentication bypass | Patient portal  | High     |
| 4 | Weak PDF passwords                                               | Patient reports | High     |
| 5 | Sensitive metadata in PDF                                        | Patient report  | Medium   |
| 6 | Publicly accessible legacy backup directory                      | `/old/`         | Critical |
| 7 | Sensitive database information stored in exposed backup          | Database backup | Critical |

---

# 🔴 Critical Findings

## 1. SQL Injection in Authentication

The login application did not properly handle user-controlled input.

This allowed SQL injection testing to demonstrate that the authentication mechanism could be bypassed.

### Impact

An attacker could potentially:

* Circumvent authentication
* Access restricted functionality
* Retrieve protected information
* Continue the attack against other application resources

### Recommendation

Implement:

* Parameterized queries
* Prepared statements
* Server-side input validation
* Secure error handling
* Proper database permissions

---

## 2. Publicly Accessible Database Backup

A legacy database backup was accessible through a publicly reachable server directory.

### Impact

An attacker could potentially obtain:

* Employee information
* Salary information
* Shareholder information
* Other information contained within the database backup

### Recommendation

Database backups should:

* Never be stored inside a public web directory
* Be stored outside the web root
* Use strict access controls
* Be encrypted at rest
* Be removed when no longer required
* Be monitored for unauthorized exposure

---

# 🟠 High-Risk Findings

## Weak PDF Passwords

Several protected PDF files used passwords that were recoverable using authorized password dictionaries.

### Impact

Weak document passwords reduce the effectiveness of encryption.

### Recommendation

Use:

* Long unique passwords
* Randomly generated credentials
* Strong password-management practices
* Centralized access control where possible
* Secure document storage

---

## Sensitive Patient Reports

The patient reports became accessible following exploitation of the authentication vulnerability.

### Impact

Unauthorized access to medical documents can create significant confidentiality and privacy risks.

### Recommendation

Implement:

* Strong authentication
* Proper authorization checks
* Server-side access control
* Secure document storage
* Access logging
* Session management
* Protection against IDOR and direct-object access weaknesses

---

# 🟡 Medium-Risk Findings

## Username Enumeration

The login system returned different responses depending on whether the submitted username existed.

### Impact

An attacker could use the response difference to identify valid accounts.

### Recommendation

Use a generic authentication message such as:

```text
Invalid username or password.
```

The response should not reveal which authentication field was incorrect.

---

## Sensitive PDF Metadata

A PDF contained metadata that revealed information about its creator and internal server processes.

### Impact

Metadata can provide useful intelligence to attackers during reconnaissance.

### Recommendation

Before publishing or distributing documents:

* Remove unnecessary metadata
* Review document properties
* Use automated metadata-cleaning processes
* Establish secure document-handling procedures

---

# 🛠️ Remediation Plan

| Priority | Recommendation                                            |
| -------- | --------------------------------------------------------- |
| Critical | Replace vulnerable SQL queries with parameterized queries |
| Critical | Remove database backups from public web directories       |
| Critical | Disable directory listing                                 |
| Critical | Review and restrict access to sensitive files             |
| High     | Strengthen document encryption and password policies      |
| High     | Implement robust authentication and authorization         |
| High     | Store patient documents outside the public web root       |
| Medium   | Prevent username enumeration                              |
| Medium   | Remove unnecessary PDF metadata                           |
| Medium   | Regularly scan for exposed backups and sensitive files    |

---

# 🧰 Tools Used

The assessment involved a range of common cybersecurity and analysis tools.

| Tool / Technology           | Purpose                                 |
| --------------------------- | --------------------------------------- |
| Web Browser                 | Application assessment                  |
| cURL                        | HTTP and reconnaissance testing         |
| Nmap                        | Network reconnaissance                  |
| PDF analysis tools          | Document security assessment            |
| Password-recovery utilities | Authorized password-strength assessment |
| `qpdf`                      | Authorized PDF processing               |
| `exiftool`                  | Metadata analysis                       |
| SQL/database analysis       | Backup assessment                       |
| ChatGPT                     | Data organization and analysis          |
| Git/GitHub                  | Project documentation                   |

---

# 📊 Risk Rating Method

Findings were categorized according to their potential security impact:

### 🔴 Critical

Vulnerabilities capable of causing severe confidentiality, integrity, or availability consequences.

### 🟠 High

Vulnerabilities that could provide significant unauthorized access or sensitive information exposure.

### 🟡 Medium

Vulnerabilities that provide useful information to an attacker or increase the likelihood of a successful attack.

### 🟢 Low

Issues with limited direct impact but which should still be addressed as part of security hardening.

---

# 📝 Professional Report Structure

The final penetration-testing report was organized into four major sections.

## 01 — Executive Summary

A high-level explanation of:

* Engagement purpose
* Scope
* Major findings
* Overall security impact

## 02 — Scope & Methodology

Documentation of:

* Target
* Testing type
* Authorized scope
* Methodology
* Tools
* Limitations

## 03 — Findings & Evidence

Each vulnerability documented with:

* Description
* Affected component
* Technical evidence
* Impact
* Risk rating
* Supporting screenshots

## 04 — Recommendations

Actionable remediation steps for each finding.

---

# 📸 Evidence

Screenshots should be stored in the repository to demonstrate the work completed during the assessment.

Suggested structure:

```text
screenshots/
│
├── 01-reconnaissance/
│   ├── robots-txt.png
│   └── application-discovery.png
│
├── 02-authentication/
│   ├── login-page.png
│   └── authentication-testing.png
│
├── 03-patient-reports/
│   ├── patient-portal.png
│   └── reports-access.png
│
├── 04-file-analysis/
│   ├── pdf-analysis.png
│   └── metadata-analysis.png
│
├── 05-backup-exposure/
│   ├── directory-listing.png
│   └── backup-discovery.png
│
└── 06-report/
    └── findings-summary.png
```

> Do not upload real credentials, secrets, private patient information, or unnecessary sensitive data to a public repository.

---

# 🧠 Key Lessons Learned

This project provided practical experience in several areas of penetration testing.

### 1. Reconnaissance Matters

Information that appears insignificant during reconnaissance can become important later in an assessment.

### 2. Authentication Errors Can Leak Information

Different login responses can allow attackers to determine whether accounts exist.

### 3. Input Validation Is Critical

Applications should never directly trust user-controlled input when constructing database queries.

### 4. Encryption Does Not Guarantee Security

Encrypted files can still be vulnerable when weak passwords are used.

### 5. Metadata Can Reveal Internal Information

File metadata should be considered part of the organization's attack surface.

### 6. Backups Must Be Protected

Old backups should never remain publicly accessible.

### 7. Vulnerabilities Can Be Chained

The most important lesson from this exercise was understanding how multiple weaknesses can connect:

```text
Recon
  ↓
Authentication weakness
  ↓
Unauthorized access
  ↓
Sensitive files
  ↓
Metadata clue
  ↓
Backup exposure
  ↓
Database information disclosure
```

---

# 🎓 Skills Demonstrated

This project demonstrates practical exposure to:

* Web application penetration testing
* Black-box security testing
* Reconnaissance
* Authentication testing
* SQL injection identification
* Vulnerability assessment
* Access-control analysis
* PDF security analysis
* Metadata analysis
* Backup exposure assessment
* Sensitive information discovery
* Risk classification
* Security documentation
* Penetration-testing reporting
* Remediation planning

---

# 📁 Repository Structure

```text
NETWORKWALKS-WEEK4-MEDIROZA-PENTEST/
│
├── README.md
│
├── screenshots/
│   ├── 01-reconnaissance/
│   ├── 02-authentication/
│   ├── 03-patient-reports/
│   ├── 04-file-analysis/
│   ├── 05-backup-exposure/
│   └── 06-report/
│
├── evidence/
│   └── [sanitized evidence only]
│
└── report/
    └── penetration-testing-report.pdf
```

---

# 📋 Project Checklist

| Milestone | Task                                | Status      |
| --------- | ----------------------------------- | ----------- |
| M1        | Reconnaissance                      | ✅ Completed |
| M1        | Authentication assessment           | ✅ Completed |
| M1        | Identify application weakness       | ✅ Completed |
| M1        | Retrieve authorized test reports    | ✅ Completed |
| M2        | Assess PDF protection               | ✅ Completed |
| M2        | Authorized password recovery        | ✅ Completed |
| M3        | Analyze PDF metadata                | ✅ Completed |
| M3        | Investigate legacy directory        | ✅ Completed |
| M3        | Identify exposed database backup    | ✅ Completed |
| M3        | Analyze database exposure           | ✅ Completed |
| M4        | Document vulnerabilities            | ✅ Completed |
| M4        | Assign risk ratings                 | ✅ Completed |
| M4        | Develop remediation recommendations | ✅ Completed |
| M4        | Produce penetration-testing report  | ✅ Completed |

---

# 🔐 Ethical & Legal Notice

This repository documents work performed as part of an **authorized cybersecurity training exercise**.

All testing was conducted within the scope defined by the NetworkWalks exercise.

Penetration-testing techniques should only be performed when:

1. Explicit authorization has been provided.
2. The target is clearly defined.
3. The testing scope is understood.
4. Testing limitations are respected.
5. Sensitive information is handled securely.

Unauthorized security testing may cause harm and may violate applicable laws.

---

# 👤 Author

## Kitenge Kiayima Jules

**Computer Science Student | Cybersecurity | AI & Machine Learning**

Africa University
Zimbabwe

GitHub: `github.com/juleskkayima`

LinkedIn: `linkedin.com/in/juleskitengek/`

---

# 🏆 Project Status

**Completed — NetworkWalks Batch B083 | Week 4**

This project strengthened my practical understanding of web application penetration testing, vulnerability assessment, information disclosure, attack-chain analysis, and professional cybersecurity reporting.

---

## 🙏 Acknowledgements

Special thanks to **NetworkWalks** for providing a controlled environment for practical cybersecurity training.

**NetworkWalks — Penetration Testing Project**
**Mediroza General Hospital**
**Batch B083 | Week 4**

