1. Server: Apache/2.4.63 (Ubuntu)
           Meaning: identifies the web server and version.
           Risk: Knowing the server/version helps attackers find targeted exploits.
           Fix: Keep Apache up to date; remove or limit version banners if required by policy.

2 . Cookie security created without the httponly flag / PHPSESSID without httponly
           Meaning: Cookies are accessible from client-side scripts (JS).
           Risk: XSS could steal session cookies.
           Fix: Set HttpOnly on session cookies (PHP: session.cookie_httponly = 1 in php.ini; for frameworks, set cookie flags).

3. Missing X-Frame-Options header (anti-clickjacking)
           Meaning: Page can be framed by other sites.
           Risk: Clickjacking attacks are possible.
           Fix: Add header X-Frame-Options: SAMEORIGIN or use Content-Security-Policy frame-ancestors.

4. Root page redirects to login.php
          Meaning: Normal for apps that require authentication; note for report only.

5. ETags leaking inode info (ETag header values)
          Meaning: ETags expose file change/inode info.
          Risk: Fingerprinting or cache side-channels.
          Fix: Disable ETags in Apache (FileETag None) or sanitize them.

6. robots.txt entry returned non-forbidden/redirect (302)
          Meaning: robots.txt exists and contains entries; review it as it may reveal hidden paths.
          Risk: Attackers can use paths in robots.txt for reconnaissance.
          Fix: Don’t list sensitive admin paths in robots.txt; protect them properly.

7. Allowed HTTP Methods: GET, POST, OPTIONS, HEAD
          Meaning: OPTIONS allowed — okay; ensure PUT/DELETE not enabled.
          Risk: If unsafe methods (PUT/DELETE) are enabled, it may allow file upload or deletion.
          Fix: Restrict HTTP methods to only what the app needs (typically GET, POST, HEAD).

8. Directory indexing found for /dvwa/config/, /dvwa/tests/, /dvwa/database/, /dvwa/docs/
          Meaning: These directories allow directory listing.
          Risk: Exposes file lists and possibly sensitive files (config, SQL dumps, tests).
          Fix: Disable directory listing (Apache Options -Indexes) and remove or protect sensitive dirs; restrict access via .htaccess or server config.

9. /dvwa/config/: Configuration information may be available
          Meaning: the config folder may expose sensitive configuration files.
          Risk: Exposure of DB credentials or config data.
          Fix: Move config outside web root or restrict access (deny from all) and ensure config files are not world-readable.

10. /dvwa/tests/ and /dvwa/database/: interesting or contains DB info
          Meaning: Tests and database directories may reveal sample data or SQL files.
          Risk: Could leak DB schema, credentials, or seed data.
          Fix: Remove test/demo directories from production; ensure only in test environments.

11. /dvwa/.git/index: Git index accessible
          Meaning: .git folder or index file is accessible from the web.
          Risk: Attackers can download the repo, history, or sensitive files (secrets).

Fix: Never expose .git; remove .git from webroot or restrict access. If you need repo on host, store outside /var/www/html or disable access with server rules.

Admin login page found (/dvwa/login.php)

Meaning: expected; ensure brute-force protection and multi-factor on real deployments.
