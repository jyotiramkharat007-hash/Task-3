# Task-3

# Nikto Vulnerability Scan Report

**Scan Date:** 10-Aug-2025  
**Nikto Version:** 2.5.0  
**Target:** `http://192.168.243.87`  
**IP Address:** `192.168.243.87`  
**Port:** 80  
**Server:** Apache/2.4.63 (Debian)  
**Scan Duration:** 21 seconds  

---

## Findings

1. **Missing Security Header: X-Frame-Options**  
   - The anti-clickjacking `X-Frame-Options` header is not present.  
   - **Impact:** The website could be embedded in an iframe by attackers to perform clickjacking attacks.  
   - **Reference:** [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)  

2. **Missing Security Header: X-Content-Type-Options**  
   - The `X-Content-Type-Options` header is not set.  
   - **Impact:** May allow MIME type sniffing attacks.  
   - **Reference:** [Netsparker Article](https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/)  

3. **ETag Information Leakage**  
   - Server may leak inode numbers via ETags (e.g., inode: 29cf, size: 63bdba3d90b74, mtime: gzip).  
   - **Impact:** Could allow attackers to infer sensitive file information.  
   - **CVE Reference:** [CVE-2003-1418](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2003-1418)  

4. **HTTP Methods Allowed**  
   - Supported methods: `HEAD, GET, POST, OPTIONS`  
   - **Impact:** Unused HTTP methods might open attack vectors if misconfigured.  

5. **Apache Server Status Page Exposed**  
   - Path: `/server-status` is accessible.  
   - **Impact:** Reveals sensitive server statistics and configurations.  
   - **Recommendation:** Restrict access to trusted IPs or disable in Apache config.  
   - **Reference:** OSVDB-561  

---

## Summary
- **Total Requests:** 8102  
- **Errors:** 0  
- **Vulnerabilities Found:** 5  

---

## Recommendations
- Add `X-Frame-Options` header.
- Add `X-Content-Type-Options` header.
- Disable or restrict `/server-status` page.
- Remove ETag header or configure to avoid leaking inode numbers.
- Review allowed HTTP methods and disable unnecessary ones.

---

**Note:** Nikto reported that parts of the server headers are newer than its database. Attempt to update failed; consider manually notifying `sullo@cirt.net`.
