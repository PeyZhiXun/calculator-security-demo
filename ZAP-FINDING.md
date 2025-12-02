## 🔍 ZAP Findings Interpretation

Below is a clear summary of all WARN-NEW findings (Medium + Low severity) from the ZAP Full Scan.

---

### ⚠️ Medium Severity Issues

| Code   | Issue                                   | Why It Matters                                         |
|--------|------------------------------------------|---------------------------------------------------------|
| 10038  | Content Security Policy (CSP) Not Set     | No CSP → higher risk of **XSS** attacks.                |
| 10106  | HTTP Only Site                           | HTTP not encrypted → data can be **intercepted**.       |
| 10020  | Missing Anti-Clickjacking Header         | Allows **clickjacking** attacks via malicious frames.  |

#### Affected URLs
**10038 – CSP Not Set**
- http://localhost:5000/
- http://localhost:5000/favicon.ico
- http://localhost:5000/robots.txt
- http://localhost:5000/sitemap.xml

**10106 – HTTP Only Site**
- http://localhost:5000/calculate

**10020 – Missing Anti-Clickjacking Header**
- http://localhost:5000/
- http://localhost:5000/

---

### 🔽 Low Severity Issues

| Code   | Issue                                   | Why It Matters                                                |
|--------|------------------------------------------|----------------------------------------------------------------|
| 90004  | Insufficient Site Isolation (Spectre)    | Missing isolation → **Spectre** side-channel risk.             |
| 10063  | Permissions Policy Header Not Set        | May allow access to mic/camera/location.                      |
| 10036  | Server Version Information Leaked        | Reveals versions → helps attackers find exploits.             |
| 10021  | X-Content-Type-Options Missing           | No `nosniff` → increased **XSS** risk.                        |

#### Affected URLs
**90004 – Spectre Isolation**
- http://localhost:5000/
- (multiple similar policy checks on root)

**10063 – Permissions Policy Missing**
- http://localhost:5000/
- http://localhost:5000/favicon.ico
- http://localhost:5000/robots.txt
- http://localhost:5000/sitemap.xml

**10036 – Server Version Leaked**
- http://localhost:5000/
- http://localhost:5000/favicon.ico
- http://localhost:5000/robots.txt
- http://localhost:5000/sitemap.xml
- http://localhost:5000/calculate

**10021 – X-Content-Type-Options Missing**
- http://localhost:5000/
- http://localhost:5000/

