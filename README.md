# Web Application Security Assessment: Stored & Reflected XSS Analysis

## 🏢 Project Overview
Conducted as part of a proactive security engagement by **SkyLock Cyber Defense**, this project evaluates the resilience of a legacy HR management platform (simulated via **DVWA - Damn Vulnerable Web Application**) prior to an upcoming compliance audit. 

The primary objective was not merely to exploit vulnerabilities (Stored and Reflected Cross-Site Scripting), but to perform a deep-dive security analysis across varying defensive postures (**Low**, **Medium**, and **Impossible** security levels). By combining active exploitation using Burp Suite with static source code review, this assessment documents how modern defensive controls mitigate application-layer attacks.

---

## 🛠️ Tools & Environment
* **Testing OS:** Kali Linux (Virtual Machine)
* **Target Application:** DVWA (Damn Vulnerable Web Application)
* **Proxy & Analysis:** Burp Suite Community Edition
* **Browser & Inspector:** Mozilla Firefox & Browser DevTools
* **Compliance Standard:** OWASP Top 10 (A03:2021 - Injection / Cross-Site Scripting)

---

## 🔍 Methodology & Security Tier Analysis

### 1. Reflected XSS Assessment
* **Low Security:** No input sanitization or output encoding. Payloads injected via URL parameters executed immediately in the browser context.
* **Medium Security:** Utilizes basic string replacement (`str_replace`) to strip `<script>` tags. 
  * *Bypass:* Case variation (`<sCrIpT>`) or nested tag injection (`<scr<script>ipt>`) often bypassed naive filters on vulnerable implementations.
* **Impossible Security:** Implements robust context-aware output encoding via `htmlspecialchars()` combined with PHP anti-CSRF/session tokens to guarantee safe rendering.

### 2. Stored XSS Assessment
* **Low Security:** Direct database insertion and retrieval without sanitization, leading to persistent code execution for all users viewing the vulnerable input fields (e.g., Guestbook).
* **Medium Security:** Applies `strip_tags()` and `addslashes()`, neutralizing raw HTML tags but occasionally leaving attribute-based contexts vulnerable if improperly escaped.
* **Impossible Security:** Employs strict database parameterization (Prepared Statements) alongside strict type-casting and `htmlspecialchars()` during output rendering, completely severing the bridge between data storage and script execution.

---

## 📂 Repository Structure
```text
├── report/
│   └── Penetration_Testing_Report.pdf  # Formal assessment report
├── src/
│   └── code_analysis_notes.md          # Source code mitigation comparisons
└── README.md
