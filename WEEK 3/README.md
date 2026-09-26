# NetworkWalks Week 3 – Password Cracking README

**Program:** Cybersecurity & Ethical Hacking Internship – NetworkWalks Academy
**Week:** 3
**Focus:** Password Cracking with John the Ripper & NetworkWalks Browser Tools

> **Disclaimer:** All activities in this project were performed exclusively on training files supplied by NetworkWalks Academy, within an authorised laboratory environment. No unauthorized systems, accounts, or files were accessed. This repository is for educational and portfolio purposes only.

## Overview

This project documents the Week 3 practical exercises for the NetworkWalks Academy cybersecurity internship, focused on **password cracking and password recovery for encrypted PDF documents**. The goal was to understand how security professionals test password strength using offline hash-based recovery techniques, and to apply that knowledge through two independent toolchains — one local, one browser-based.

## Objectives

- Understand the concept and purpose of password cracking
- Distinguish between an encrypted file and a crackable hash representation
- Install and configure **John the Ripper (Jumbo)** and the **Johnny GUI**
- Extract a PDF-compatible hash from a password-protected document
- Perform a controlled, offline password-recovery attack
- Use **NetworkWalks'** browser-based hash extraction and cracking laboratory
- Validate recovered passwords by successfully opening the original protected files
- Document findings and defensive security recommendations

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| **John the Ripper (Jumbo)** | Offline password-hash cracking engine |
| **Johnny** | Graphical front-end for John the Ripper |
| **pdf2john-based hash extractor** | Converts an encrypted PDF into a crackable `$pdf$` hash |
| **NetworkWalks Hash Calculator** | Browser-based PDF hash extraction |
| **NetworkWalks Password Cracker** | Browser-based candidate testing engine |

## Target Files

The following files were provided for this lab:

- `My Locked PDF1.pdf`
- `My Locked PDF2.pdf`
- `My Locked PDF3.pdf`
- `W3-PM1 - Week3 - Project Module1 - Password Cracking with JTR.pdf`
- `W3-PM2 - Week3 - Project Module2 - Password Cracking with NetworkWalks Tools.pdf`
- `z. Week3 Projects v1.pdf`

## Module Summary

| Module | Toolchain | Target | Recovered Password |
|--------|-----------|--------|-------------------|
| **Module One** | John the Ripper + Johnny (local) | Locked PDF 3 | `1qaz2wsx` |
| **Module Two** | NetworkWalks Hash Calculator + Password Cracker (web) | Locked PDF 2 | `password1` |

**Workflow (both modules):** Encrypted PDF → Hash extraction (`$pdf$`) → Password-candidate testing → Recovered password → Validation

## Module One — John the Ripper & Johnny

### What is John the Ripper?

John the Ripper (JTR) is a free, open-source password cracking tool supporting many hash types and password formats. It is known for its flexibility, auto-detection capabilities, and extensive rule system. It started as a tool for Unix systems but now works on Windows, Linux, and Mac, and can unlock password-protected files like PDF, ZIP, and Office documents.

### What is Johnny?

**Johnny** is the graphical version of John the Ripper. It gives a simple point-and-click interface, allowing beginners to use JTR without typing long commands.

### Steps

1. **Install John the Ripper (Jumbo)** on Windows or Kali Linux.
2. **Extract the hash** from the locked PDF using a `pdf2john`-based extractor, producing a `$pdf$` hash.
3. **Run John the Ripper** against the extracted hash:
   ```bash
   john --wordlist=rockyou.txt pdf_hash.txt
   ```
4. **Alternatively, use Johnny GUI** to load the hash file, select the wordlist, and start the attack.
5. **View the cracked password** once the attack completes.

### Basic JTR Commands Reference

| Command | Purpose |
|---------|---------|
| `john hashes.txt` | Auto-detect hash type and crack |
| `john --wordlist=rockyou.txt hashes.txt` | Specify a wordlist |
| `john --format=raw-md5 hashes.txt` | Specify hash format explicitly |
| `john --show hashes.txt` | Show cracked passwords |
| `john --list=formats` | List all supported hash formats |

## Module Two — NetworkWalks Browser Tools

### What are NetworkWalks Tools?

NetworkWalks Tools are free online tools that allow users to extract crackable hashes from PDF files and perform dictionary attacks directly in a web browser without installing anything.

### NetworkWalks Hash Calculator

- **URL:** https://networkwalks.com/hash-calculator/
- **Purpose:** Browser-based PDF hash extraction. Upload the locked PDF, and the tool extracts the crackable `$pdf$` hash. All processing occurs client-side in the browser.

### NetworkWalks Password Cracker

- **URL:** https://networkwalks.com/password-cracker/
- **Purpose:** Browser-based dictionary attack engine. Paste the extracted hash, and the tool hashes every word in a wordlist to match it against the PDF password hash — the same idea John the Ripper uses.
- **Built-in list:** 100 passwords included; custom wordlists can also be uploaded.

### Steps

1. **Download the encrypted PDF file** (`My Locked PDF2.pdf`).
2. **Open the NetworkWalks Hash Calculator** in a web browser.
3. **Upload the locked PDF** to the Hash Calculator. The tool will read the file and provide the hash value starting with `$pdf$`.
4. **Copy the complete hash** starting from `$pdf$` — do not miss any part of it.
5. **Open the NetworkWalks Password Cracker** in a web browser.
6. **Paste the hash value** into the Password Cracker and start the attack.
7. **Wait for the tool to finish.** The cracked password will be shown on the screen.
8. **Open the locked PDF file** and enter the cracked password.

## Key Findings

- Weak, predictable, or keyboard-pattern passwords (`1qaz2wsx`, `password1`) can be recovered quickly through offline attacks.
- Password **length, uniqueness, and unpredictability** are far more important defensive factors than the mere presence of a password.
- Offline cracking means an attacker doesn't need repeated access to the original file once a hash is obtained — protecting hashes and encrypted backups matters as much as protecting the passwords themselves.
- A tool reporting a "successful crack" should always be validated by actually opening the original protected file.

## Defensive Recommendations

- Use long, unique, unpredictable passwords — avoid keyboard patterns and common words
- Adopt a password manager for generation and secure storage
- Enable multi-factor authentication (MFA) where possible
- Protect hash files and encrypted backups as rigorously as plaintext passwords
- Regularly audit password strength across systems

## References

- NetworkWalks Hash Calculator: https://networkwalks.com/hash-calculator/
- NetworkWalks Password Cracker: https://networkwalks.com/password-cracker/
- NetworkWalks Password Cracking Lab: https://networkwalks.com/password-cracking-with-networkwalks-tools-project-task-lab/
- John the Ripper: https://www.openwall.com/john/

## Author

**Intern Name:** [Kitenge Kiayima Jules]
**Program:** Cybersecurity Training at NetworkWalks Academy
**Date:** 26 september 2026
