# Session Hijacking — DVWA & OWASP Juice Shop

## Overview
This project demonstrates session hijacking attacks on two intentionally 
vulnerable web applications: DVWA and OWASP Juice Shop. The goal is to 
understand how poor session management can be exploited and how to defend 
against it.

## Tools Used
- Burp Suite Community Edition
- Kali Linux (VMware)
- Firefox Developer Tools
- DVWA (Damn Vulnerable Web Application)
- OWASP Juice Shop (via Docker)

## What Was Tested
- Cookie attribute inspection (HttpOnly, Secure, SameSite)
- Session ID capture and reuse
- PHPSESSID manipulation on DVWA
- Token-based session hijacking on OWASP Juice Shop

## Attack Flow — DVWA
1. Logged into DVWA as victim, captured PHPSESSID via DevTools
2. Opened attacker browser (Burp Suite browser)
3. Replaced attacker's PHPSESSID with victim's session ID
4. Gained unauthorized access to victim's account without credentials

## Attack Flow — OWASP Juice Shop
1. Logged in as victim (admin), copied session token from cookies
2. Logged in as attacker (Jim) in separate browser
3. Replaced attacker's token with victim's token
4. Successfully hijacked admin session

## Key Findings
- DVWA (Low security): No session regeneration on login, predictable IDs
- OWASP Juice Shop: Missing Secure and SameSite cookie attributes

## Recommendations
- Use HttpOnly + Secure flags on all session cookies
- Regenerate session ID after login
- Implement session timeout and invalidation on logout
- Enforce HTTPS everywhere

## References
- https://owasp.org/www-community/attacks/Session_hijacking_attack
- https://portswigger.net/burp/communitydownload
