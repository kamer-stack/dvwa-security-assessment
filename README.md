# 🛡️ DVWA Security Assessment — AI-Assisted Penetration Test

> A comprehensive security assessment of DVWA across 13 vulnerability modules at Low, Medium, and High security levels, using HexStrike AI tooling integrated with Cursor AI via MCP, and automated Python exploit scripts.

![Security](https://img.shields.io/badge/Category-Penetration%20Testing-red)
![Tools](https://img.shields.io/badge/Tools-HexStrike%20%7C%20Cursor%20AI%20%7C%20Python-blue)
![Modules](https://img.shields.io/badge/Modules%20Tested-13-orange)
![Vuln Rate](https://img.shields.io/badge/Overall%20Vuln%20Rate-77%25-critical)
![Institution](https://img.shields.io/badge/Institution-PUCIT-green)

---

## 📋 Overview

This project presents a full-scope penetration test of a locally hosted DVWA (Damn Vulnerable Web Application) instance. The assessment was conducted using an AI-assisted methodology — HexStrike AI integrated with the Cursor AI editor via the Model Context Protocol (MCP) — combined with custom Python exploit scripts generated and executed against each target module.

The assessment covers **13 vulnerability categories** across **3 security levels** (Low, Medium, High), producing a professional-grade security report with findings, evidence, exploit scripts, and remediation guidance.

---

## 📊 Executive Summary

Of 39 total vulnerability configurations tested (13 modules × 3 levels), **30 were exploitable** — a **77% overall vulnerability rate**.

| Security Level | Vulnerable Modules | Hardened Modules | Vulnerability Rate |
|----------------|-------------------|------------------|--------------------|
| Low | 12 | 1 | 92% |
| Medium | 12 | 1 | 92% |
| High | 6 | 7 | 46% |

**Critical findings confirmed:** Command Injection, SQL Injection, and unrestricted File Upload at Low and Medium levels. Brute Force, CSRF, and DOM XSS remained exploitable even at High security.

---

## 🎯 Vulnerability Modules Tested

| Module | Low | Medium | High |
|--------|-----|--------|------|
| Brute Force | ✅ Vulnerable | ✅ Vulnerable | ✅ Vulnerable |
| Command Injection | ✅ Vulnerable | ✅ Vulnerable | 🛡️ Mitigated |
| CSRF | ✅ Vulnerable | ✅ Vulnerable | ✅ Vulnerable |
| File Inclusion (LFI) | ✅ Vulnerable | ✅ Vulnerable | 🛡️ Mitigated |
| File Upload | ✅ Vulnerable | ✅ Vulnerable | ✅ Vulnerable |
| SQL Injection | ✅ Vulnerable | ✅ Vulnerable | 🛡️ Mitigated |
| SQL Injection (Blind) | ✅ Vulnerable | ✅ Vulnerable | 🛡️ Mitigated |
| XSS (Reflected) | ✅ Vulnerable | ✅ Vulnerable | ✅ Vulnerable |
| XSS (Stored) | ✅ Vulnerable | ✅ Vulnerable | 🛡️ Mitigated |
| XSS (DOM) | ✅ Vulnerable | ✅ Vulnerable | ✅ Vulnerable |
| Weak Session IDs | ℹ️ Info | ✅ Vulnerable | ✅ Vulnerable |
| JavaScript Attacks | ✅ Vulnerable | 🛡️ Mitigated | 🛡️ Mitigated |
| Open HTTP Redirect | ℹ️ Not in v1.10 | ℹ️ Not in v1.10 | ℹ️ Not in v1.10 |

---

## 🔑 Notable Findings

**File Upload — High Security Bypass**  
The High level was bypassed using a double-extension file (`shell.php.png`) with GIF magic bytes prepended — exploiting misconfigured file type detection that checked only the first bytes and the final extension.

**CSRF — High Security Bypass**  
High security required a valid CSRF token, but since the token was obtainable within the same session, a real-world attacker hosting a malicious page visited by a logged-in victim could still exploit it.

**DOM XSS — All Three Levels**  
Vulnerable JavaScript sinks (`document.write`, `innerHTML`) were confirmed at all three security levels — DOM XSS was never fully mitigated.

---

## 🐍 Exploit Script Inventory

39 Python exploit scripts were generated and executed, one per module per security level. All scripts are self-contained and target a specific vulnerability at a specific level.

```
exploits/
├── brute_force_low.py
├── brute_force_medium.py
├── brute_force_high.py
├── command_injection_low.py
├── command_injection_medium.py
├── command_injection_high.py
├── csrf_low.py
├── csrf_medium.py
├── csrf_high.py
├── file_inclusion_low.py
├── file_inclusion_medium.py
├── file_inclusion_high.py
├── file_upload_low.py
├── file_upload_medium.py
├── file_upload_high.py
├── sql_injection_low.py
├── sql_injection_medium.py
├── sql_injection_high.py
├── sql_injection_blind_low.py
├── sql_injection_blind_medium.py
├── sql_injection_blind_high.py
├── xss_reflected_low.py
├── xss_reflected_medium.py
├── xss_reflected_high.py
├── xss_stored_low.py
├── xss_stored_medium.py
├── xss_stored_high.py
├── xss_dom_low.py
├── xss_dom_medium.py
├── xss_dom_high.py
├── weak_session_ids_low.py
├── weak_session_ids_medium.py
├── weak_session_ids_high.py
├── javascript_attacks_low.py
├── javascript_attacks_medium.py
├── javascript_attacks_high.py
├── open_http_redirect_low.py
├── open_http_redirect_medium.py
└── open_http_redirect_high.py
```

---

## 🔧 Top Remediation Recommendations

1. Replace all string-concatenation SQL queries with **prepared statements**
2. Disable `shell_exec`, `exec`, `system` in `php.ini` — use allowlists where shell access is necessary
3. Deploy **Content-Security-Policy** headers and context-aware output encoding for all XSS vectors
4. Implement **anti-CSRF tokens** with server-side validation on all state-changing operations
5. Validate uploaded file **magic bytes** server-side — never trust extension or MIME type alone
6. Use **cryptographically random session IDs** with at least 128 bits of entropy
7. Implement **rate limiting, account lockout, and CAPTCHA** on all authentication endpoints

---

## 📁 Repository Structure

```
dvwa-security-assessment/
├── README.md
├── report/
│   └── DVWA_Security_Assessment_Khadija_Amer.pdf
└── exploits/
    └── (39 Python exploit scripts)
```

---

## ⚠️ Disclaimer

All testing was performed exclusively on a locally hosted DVWA instance running in an isolated Docker environment. No real systems, users, or networks were targeted. This project is strictly for educational purposes.

---

## 👩‍💻 Author

**Khadija Amer**  
Punjab University College of Information Technology (PUCIT)  
Course: Information Security | Spring 2026  
Instructor: Sir Shehryar Raza
