OIBSIP_CyberSecurity_Task7

Task Title: Vulnerability Scanning with Nikto

Intern Name: Ellis Gbewordo
Date: 2025-11-03

Objective
Use Nikto to scan a web server and report potential vulnerabilities and misconfigurations.

Tools
Nikto, Apache, DVWA (lab)

Steps performed
1. Installed Nikto with: sudo apt install nikto
2. Ran Nikto against the DVWA lab: nikto -h http://127.0.0.1/dvwa -output nikto_scan_results.txt
3. Reviewed findings and recommended mitigations.

Key findings (summary)
- Directory indexing present for /dvwa/config/, /dvwa/tests/, /dvwa/database/, /dvwa/docs/
- Exposed .git index file at /dvwa/.git/index
- Cookies (security and PHPSESSID) are missing the HttpOnly flag
- Missing X-Frame-Options header
- ETag header leaking inode information
- robots.txt contains entries and root redirects to login.php
- Allowed HTTP methods include OPTIONS (verify methods allowed)
- Admin login page detected at /dvwa/login.php

Recommendations
- Disable directory listing (Options -Indexes) and remove test directories from webroot
- Remove or restrict access to .git and any config/database files
- Set session cookies with HttpOnly and Secure flags
- Add security headers (X-Frame-Options, X-Content-Type-Options, Content-Security-Policy)
- Disable ETags or configure them properly
- Limit HTTP methods to the required ones only
- Review robots.txt entries and avoid listing sensitive paths

Files included
- nikto_scan_results.txt
- README.md
- (Optional) screenshots/nikto_scan.png

Notes
This scan was performed in a local lab environment (DVWA) for educational purposes only. Do not scan systems you do not own or have permission to test.
