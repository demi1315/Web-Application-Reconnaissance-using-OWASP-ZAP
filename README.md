# 🕷️ Web Application Reconnaissance using OWASP ZAP  
Attack → Defense Narrative on OWASP Juice Shop

---

## 📌 Executive Summary

This project documents a **hands-on web application reconnaissance and vulnerability assessment** performed using **OWASP ZAP** against **OWASP Juice Shop**, an intentionally vulnerable application created for security training.

The objective was to simulate **real-world attacker reconnaissance**, identify vulnerabilities aligned with the **OWASP Top 10**, and then transition into a **defender’s mindset** by analyzing impact and recommending mitigations.

All activities were conducted in a **controlled lab environment** and strictly for **educational and ethical purposes**.

---

## 🎯 Why This Project Exists

Modern web attacks rarely begin with exploitation.  
They begin with **reconnaissance**.

This project exists to demonstrate:

- how attackers map applications before exploitation
- how automated tools accelerate discovery
- how misconfigurations amplify risk
- why early detection and secure defaults matter

---

## 🧱 Target Environment

**Application**
- OWASP Juice Shop (intentionally vulnerable)

**Deployment**
- Docker container
- Exposed on `http://localhost:3000`

**Testing Tool**
- OWASP ZAP (Kali Linux)

This setup ensures **safe, legal, and repeatable testing**.

---

## 🟥 Attacker Perspective (Reconnaissance & Discovery)

### 🔍 Phase 1: Application Mapping (Spider Scan)

**Goal:** Discover reachable pages, endpoints, and parameters.

**Action Performed**
- ZAP Spider scan against the application root
- Default context and unauthenticated user
- Automatic crawling of links and parameters

**Outcome**
- Hidden endpoints discovered
- Parameters populated in Sites Tree
- Expanded attack surface visibility

---

### 🕵️ Phase 2: Silent Weakness Detection (Passive Scan)

**Goal:** Identify vulnerabilities without active exploitation.

**What Happened**
- Passive Scanner analyzed HTTP/S traffic
- No malicious payloads sent
- Issues detected purely from responses

**Findings Included**
- Security misconfigurations
- Information disclosure
- Insecure cookie attributes

---

### 🚨 Phase 3: Active Vulnerability Testing (Active Scan)

**Goal:** Validate exploitable vulnerabilities.

**Action Performed**
- Active Scan using default ZAP policy
- Payloads sent to discovered endpoints
- Coverage aligned with OWASP Top 10

**Confirmed Vulnerabilities**
- SQL Injection (High)
- Cross-Site Scripting (XSS)
- Broken Access Control
- Security Misconfigurations

---

## 🟥 Key Vulnerabilities Identified (Attacker View)

### 🔴 SQL Injection (High)
- Injection into search parameter
- Potential database compromise
- Direct OWASP Top 10 risk (A03)

### 🟠 Missing Security Headers (Medium)
- No Content Security Policy (CSP)
- No Anti-Clickjacking protection
- Increased XSS and UI redress risk

### 🟠 CORS / Cross-Domain Misconfiguration (Medium)
- Overly permissive cross-origin access
- Data exposure to untrusted domains

### 🟠 Session ID in URL (Medium)
- Session tokens exposed in query strings
- Risk of session hijacking via logs/history

### 🟠 Vulnerable JavaScript Libraries (Medium)
- Outdated jQuery version
- Known CVEs
- Supply-chain attack potential

### 🟡 Information Disclosure (Low)
- Internal IP addresses
- Timestamps
- Suspicious developer comments

---

## 🟦 Defender Perspective (Impact & Risk)

From a defensive standpoint, these issues can lead to:

- Unauthorized data access
- Account compromise
- Client-side attacks (XSS / clickjacking)
- Session hijacking
- Increased attacker efficiency during recon
- Supply-chain compromise via third-party scripts

The findings highlight how **misconfigurations are often more dangerous than code bugs**.

---

## 🛡️ Defense & Remediation Strategy

### 🔐 Input & Query Handling
- Use parameterized queries
- Apply strict input validation
- Escape user-controlled data

### 🧱 Security Headers
- Enforce Content-Security-Policy (CSP)
- Add X-Frame-Options or `frame-ancestors`
- Harden cookies (`HttpOnly`, `Secure`, `SameSite`)

### 🌐 CORS Hardening
- Avoid wildcard origins
- Restrict to trusted domains only
- Validate `Origin` server-side

### 🔑 Session Management
- Never pass session IDs in URLs
- Regenerate sessions on auth events
- Apply secure cookie attributes

### 📦 Dependency Security
- Upgrade vulnerable libraries
- Apply Subresource Integrity (SRI)
- Host critical scripts locally

### 🧹 Information Hygiene
- Remove debug output
- Eliminate internal IP exposure
- Strip sensitive comments from production code

---

## 📸 Screenshots & Evidence

The `screenshots/` directory contains:

- ZAP Spider results (Sites Tree)
- Passive Scan alerts
- Active Scan findings
- Request/response evidence
- Header and misconfiguration proof

All screenshots are taken from a **local lab environment** and sanitized.

---

## 🧠 Key Learnings

- Reconnaissance defines attack success
- Automation dramatically increases discovery speed
- OWASP ZAP is effective for both learning and testing
- Misconfigurations are high-impact, low-effort fixes
- Ethical testing is mandatory for real-world security work

---

## ⚠️ Ethical Disclosure

All testing was performed:
- On OWASP Juice Shop
- In a controlled lab environment
- With no impact on real systems

This project follows **responsible disclosure and ethical hacking principles**.

---

## 📌 Final Takeaway

Web security is not just about fixing vulnerabilities —  
it is about **reducing attack surface early through proper reconnaissance awareness, secure defaults, and continuous testing**.

---

*This project is part of my cybersecurity internship portfolio and demonstrates practical web application reconnaissance, vulnerability analysis, and defensive security thinking.*
