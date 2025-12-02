# Scanner Comparison

This document compares what each scanner (SAST, SCA, DAST) found in my project.  
The goal is to see which tool finds what type of issues.

---

## 1. Only CodeQL (SAST) Found

CodeQL looks at the source code.  
It found **1 issue**:

- The Flask app is running in **debug mode**, which is not safe for production.

DAST and SCA would not find this because it is a code-level setting, not something that happens during runtime.

---

## 2. Only ZAP (DAST) Found

ZAP tests the running application.  
It found several issues related to HTTP headers and security configurations, for example:

- CSP header missing  
- Anti-clickjacking header missing  
- X-Content-Type-Options missing  
- Permissions-Policy missing  
- App is served over HTTP instead of HTTPS  
- Server leaks version information  
- Some Spectre-related isolation headers missing

These are things you only see when the application is actually running, which is why SAST and SCA didn't detect them.

---

## 3. Only Dependency-Check (SCA) Found

SCA checks for vulnerable dependencies.

In this project, it found **0 vulnerabilities**  
(Flask 2.0.1 and Werkzeug 2.0.1 did not show any CVEs in the scan).

If there were outdated or insecure packages, SCA would detect them, but the other tools would not.

---

## 4. Overlap Between Tools

There was basically **no overlap**.  
Each tool reported completely different types of issues:

- CodeQL → 1 code issue  
- SCA → no dependency issues  
- ZAP → multiple runtime/config issues  

This makes sense because each tool focuses on a different layer:

- **SAST** → the code  
- **SCA** → the libraries you install  
- **DAST** → the running web application

---

## Summary

- **SAST** found a code configuration problem (debug mode).  
- **SCA** found no dependency problems.  
- **DAST** found several runtime security issues.  

This shows why using all three scanners together is useful—they cover different parts of the application.
