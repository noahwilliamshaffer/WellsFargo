# Wells Fargo Security Research (November - December 2024)

## Overview
This repository contains extensive security research and reconnaissance conducted on various Wells Fargo systems. The findings encompass:
- **Reconnaissance of staging environments**
- **Vulnerability scanning and penetration testing results**
- **Wayback Machine historical URL analysis**
- **Subdomain enumeration and API exposure assessments**
- **Security header analysis and authentication risks**

Each section provides an in-depth look into security risks and recommendations for remediation.

---

## Contents

### 1. Wells Fargo Research (November 2024)
- **Identified Vulnerabilities:**
  - Found weaknesses in **staging environments** that could be leveraged by attackers.
  - **CVE-2020-11023** (jQuery XSS vulnerability) was detected in certain pages.
- **Recommendations:**
  - Upgrade **jQuery to version 3.5.0+** to mitigate XSS risks.
  - Secure **staging environments** with **access control restrictions**.

### 2. Wells Fargo - Venom OSHPValidator
- **Security Header Analysis:**
  - **Strict-Transport-Security (HSTS):** Enforced, ensuring HTTPS usage.
  - **X-Frame-Options:** Set to `SAMEORIGIN`, preventing clickjacking.
  - **X-Content-Type-Options:** `nosniff`, preventing MIME-type sniffing.
  - **X-XSS-Protection:** Enabled, but should be replaced with modern **CSP policies**.
- **Recommendations:**
  - Implement a **robust Content Security Policy (CSP)** to prevent XSS attacks.
  - Review HSTS settings to **ensure all subdomains** are covered.

### 3. Wells Fargo - Subfinder
- **Subdomain Enumeration Findings:**
  - Discovered **internal services**, **mail servers**, and **financial APIs**.
  - Identified subdomains linked to **retirement and investment platforms**.
  - Potential **exposed endpoints** with **API keys** found in some responses.
- **Recommendations:**
  - Secure **internal subdomains** from external access.
  - **Monitor DNS records** to prevent subdomain takeovers.
  - Implement **rate limiting** on API endpoints to prevent abuse.

### 4. Wells Fargo - Nuance Third Party Customer Service Application
- **DNS Analysis:**
  - Identified **Nameservers (NS)**, **Mail Exchange (MX) records**, and **TXT records**.
  - Found **SPF, Google, Facebook, and MongoDB TXT verification records**.
  - **DNS Zone Transfer (AXFR) attempts were unsuccessful**, indicating secured configurations.
- **Recommendations:**
  - Regularly audit **DNS records** for misconfigurations.
  - **Restrict public exposure** of DNS TXT records where possible.

### 5. Wells Fargo - Metspolit HTTP Crawl
- **Web Application Scanning Results:**
  - Found multiple **redirects and broken links (404 errors)**.
  - Discovered **exposed directories** and **publicly accessible APIs**.
  - Identified forms vulnerable to **enumeration attacks**.
- **Recommendations:**
  - Restrict access to **unnecessary directories**.
  - Implement **rate limiting** on publicly available forms.
  - Harden **API authentication** to prevent unauthorized access.

---

# Wells Fargo Wayback Recon (November 2024)

## Overview
This section contains results from **Wayback Machine** recon, focusing on identifying:
- **Old URLs that may still be accessible**
- **Exposed endpoints that attackers might exploit**
- **Historical misconfigurations and vulnerabilities**

### 1. Notes.txt
- **Command Execution Logs for Wayback Enumeration:**
  ```bash
  ./waybackurls wellsfargo.com | tee Desktop/Wellsfargo/Wayback/urls.txt
  grep -F "=http" Wellsfargo/Wayback/urls.txt | tee Wellsfargo/Wayback/httpFiltered.txt
  ```
- **Tools Used:**
  - `waybackurls`: Extracted past URLs from the **Internet Archive**.
  - `grep -F "=http"`: Filtered URLs containing **query parameters** (possible security risks).

### 2. urls.txt
- **Extracted URLs from Wayback Machine:**
  ```
  https://www.wellsfargo.com/
  http://wellsfargo.com/
  https://wellsfargo.com/
  https://www.wellsfargo.com/%20
  https://www.wellsfargo.com/?ATCLID=204862231&SPID=44794&DB_LANG=C&DB_OEM_ID=23200
  ```
- **Findings:**
  - Several URLs point to **deprecated resources**.
  - Possible **exposed authentication pages**.

### 3. httpFiltered.txt
- **Filtered URLs with Query Parameters:**
  ```
  https://csfedportal-ext.wellsfargo.com/affwebservices/public/saml2sso?SPID=WellPoint.WellsFargo&RelayState=https://secure-gateway.anthem.com/SSOPropagator/Anthem-abcbs.jsp?Vendor=WellsFargo
  ```
- **Observations:**
  - Exposed **SAML authentication endpoints**.
  - Possible **open redirect vulnerabilities**.
- **Recommendations:**
  - Validate **authentication security** for **SAML-based logins**.
  - Conduct **fuzz testing** to detect **open redirect issues**.

---

# Wells Fargo Staging Recon (November 2024)

## Overview
This section documents **security assessments of the Wells Fargo Staging Environment**. Key objectives:
- **Identify misconfigured endpoints**
- **Analyze authentication risks**
- **Detect API and JavaScript security flaws**

### 1. Identified Endpoints
- Found several requests to **staging.wellsfargo.com**, including:
  - `/auth/login/static/js/general_alt.js` (Authentication Script)
  - `/as/target/offers/dispositions` (Internal Marketing API)
  - `/target/offers/conversations` (Exposed API endpoint)
  - **Exposed `.git/` directory**, allowing potential **source code leakage**.

### 2. Security Headers Analysis
- **Existing Headers:**
  - **X-Frame-Options:** `SAMEORIGIN` (Prevents clickjacking).
  - **X-Content-Type-Options:** `nosniff` (Blocks MIME sniffing).
  - **Strict-Transport-Security (HSTS):** Enforced.
- **Concerns:**
  - **Content Security Policy (CSP) needs improvement** to prevent **XSS vulnerabilities**.

### 3. Authentication & API Risks
- **Observed Issues:**
  - Found **API calls linked to tracking and marketing offers**.
  - Possible **session handling flaws** with SAML authentication.

### 4. Recommendations
- **Remove `.git/` directory** to prevent code exposure.
- **Enhance API security** with **proper authentication and rate limiting**.
- **Restrict staging environment access logs** from external exposure.

---

## Disclaimer
This repository is for **educational and ethical security research purposes only**. Unauthorized testing, exploitation, or misuse of sensitive environments is **strictly prohibited**. Always obtain **explicit permission** before conducting security assessments.


