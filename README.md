# Wells Fargo Security Research (November - December 2024)

## **Overview**
This repository contains security research conducted on various Wells Fargo systems using a combination of reconnaissance, vulnerability scanning, and penetration testing techniques. The documents within include findings from HTTP security tests, subdomain enumeration, DNS analysis, web crawling, and vulnerability assessments.

## **Contents**
### **1. Wells Fargo Research (November 2024)**
- Examines known vulnerabilities, including **CVE-2020-11023** (jQuery XSS).
- Identifies potential weaknesses in **staging environments**.

### **2. Wells Fargo - Venom OSHPValidator**
- Performed security validation tests using `venom`.
- Found misconfigurations in:
  - **Strict-Transport-Security** headers.
  - **X-Frame-Options** policies.
  - **Content-Security-Policy** directives (potential XSS risks).
  - **Referrer-Policy**, **Clear-Site-Data**, and other missing headers.

### **3. Wells Fargo - Subfinder**
- Used `subfinder` for **subdomain enumeration**.
- Discovered numerous Wells Fargo subdomains, including:
  - **Internal services**
  - **Mail servers**
  - **Financial APIs**
  - **Retirement and investment platforms**
- These findings indicate potential attack vectors for further security assessments.

### **4. Wells Fargo - Nuance Third Party Customer Service Application**
- DNS enumeration using `msfconsole` to find:
  - **Nameservers (NS)**
  - **Mail exchange (MX) records**
  - **Text (TXT) records** (including SPF, Google, Facebook, and MongoDB verifications)
- Attempts to perform **DNS Zone Transfer (AXFR)** were unsuccessful, indicating secured configurations.

### **5. Wells Fargo - Metspolit HTTP Crawl**
- Conducted an HTTP crawl on `wellsfargo.com` to identify:
  - Redirects and broken links (**404 errors**).
  - Exposed directories and API endpoints.
  - Publicly accessible forms, which could be **exploited for enumeration**.

## **Security Considerations**
- This research is intended for educational and security auditing purposes only.
- Any unauthorized testing of production systems **without permission** may violate ethical and legal standards.
- Organizations should **prioritize remediation** of identified weaknesses, particularly missing security headers and exposed subdomains.

## **Next Steps**
- **Verify and validate** vulnerabilities with controlled proof-of-concept (PoC) testing.
- **Assess authentication mechanisms** to prevent unauthorized access.
- **Monitor exposed subdomains** for potential abuse.
- **Ensure compliance** with security best practices, such as CSP, HSTS, and proper DNS configurations.

## **Disclaimer**
This repository is for **educational and research purposes only**. Unauthorized access, exploitation, or misuse of sensitive systems is strictly **prohibited**. Please obtain **explicit permission** before conducting security assessments on any organization’s infrastructure.
