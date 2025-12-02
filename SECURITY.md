# Security Scanning

This project includes automated security checks as part of the CI pipeline.  
The goal is to catch issues early and ensure the application stays secure as it evolves.



## 1. SAST (Static Application Security Testing using CodeQL)

SAST scans the application's **source code** without running it.

### What CodeQL checks:
- Unsafe coding patterns
- Misconfigurations (e.g., Flask debug mode)
- Potential injection risks
- Hardcoded secrets
- Data flow issues

### How it runs:
- Triggers automatically on every push or pull request
- Results are shown under **GitHub → Security → Code Scanning Alerts**



## 2. SCA (Software Composition Analysis using Dependency-Check)

SCA scans the project’s **dependencies** for known vulnerabilities (CVEs).

### What Dependency-Check checks:
- Outdated or vulnerable Python packages
- Known CVEs from public vulnerability databases
- Dependency metadata

### How it runs:
- Executes on every push
- Generates reports stored in the **`sca-reports`** artifact folder

### Current scan result:
- No vulnerable dependencies were found in this project



## 3. DAST (Dynamic Application Security Testing using OWASP ZAP)

DAST tests the **running application** by simulating external attacks.

### What ZAP checks:
- Missing or weak security headers
- HTTP/HTTPS issues
- Server configuration problems
- Runtime behavior vulnerabilities

### How it runs:
- The pipeline starts the Flask app
- ZAP Baseline and Full Scan run against it
- Reports are saved under:
  - `zap-baseline-reports`
  - `zap-fullscan-reports`



## Understanding Results

Each report provides different types of findings:

- **CodeQL** → code-level issues  
- **Dependency-Check** → dependency vulnerabilities  
- **ZAP** → runtime issues and misconfigurations  



## Reporting Vulnerabilities

If you find a security issue in this project, please report it to:

**security@example.com**
