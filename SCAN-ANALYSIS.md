# Security Scan Analysis - 2025-12-02

## DAST Results (ZAP Baseline)
- Total URLs scanned:  14
- PASS: 0 (baseline did not record PASS entries in the artifact)
- WARN-NEW: 7 warnings (3 Medium + 4 Low)
- FAIL-NEW: 0 failures

### Warning Summary
| Code  | Issue                                         | Risk |
|-------|-----------------------------------------------|------|
| 10038 | Content Security Policy (CSP) Header Not Set  | Medium |
| 10106 | HTTP Only Site                                 | Medium |
| 10020 | Missing Anti-clickjacking Header               | Medium |
| 90004 | Insufficient Site Isolation (Spectre)          | Low |
| 10063 | Permissions Policy Header Not Set              | Low |
| 10036 | Server Leaks Version Information               | Low |
| 10021 | X-Content-Type-Options Header Missing          | Low |

(Informational alerts omitted because they are not warnings.)

---

## SCA Results (Dependency Check)
- High severity: **0**
- Medium severity: **0**
- Low severity: **0**

### Vulnerable Packages
- **None found.**  
---

## SAST Results (CodeQL)
- Total issues: **1**

### Issue Breakdown
- Data flow vulnerabilities: 0  
- Injection patterns: 0  
- Hardcoded secrets: 0  
- Configuration issues: **1** (Flask debug mode enabled)

### Details
**Issue:** Flask app is run in debug mode  
**File:** `app.py`  
**Line:** 36  
**Rule:** `py/flask-debug`  
**Severity:** Medium  

**Why this is a problem:**  
Running a Flask application with debug mode enabled may allow an attacker to gain access through the Werkzeug debugger.

**Recommendation:**  
Ensure that Flask applications that are run in a production environment have debugging disabled.

```python
app.run(host='0.0.0.0', port=5000, debug=False)

## Recommendations
1. **Add missing security headers**  
   - Fixes Medium/Low findings (10020, 10021, 10038, 10063).

2. **Use HTTPS instead of HTTP**  
   - Fixes 10106 (HTTP Only Site).

3. **Remove or modify server headers**  
   - Fixes 10036.

4. **Continue running SCA regularly**  
   - Even though no CVEs were found this time, new vulnerabilities may appear.

5. **Monitor CodeQL results in GitHub Security Tab**  
   - Ensure no new findings appear when code changes.

