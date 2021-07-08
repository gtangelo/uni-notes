---
fontfamily: Calibri
toc: true
---

# Glossary of Terms

Definitions for these terms were taken from [owasp.org](https://owasp.org/)

| Terms                                | Definition                                                   |
| ------------------------------------ | ------------------------------------------------------------ |
| SQL Injection (SQLi)                 | A SQL injection attack consists of insertion or “injection” of a SQL query via the input data from the client to the application. |
| Server-Side Request Forgery (SSRF)   | In a Server-Side Request Forgery (SSRF) attack, the attacker can abuse functionality on the server to read or update internal resources. |
| Cross-Site Scripting (XSS)           | Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. |
| Stored XSS Attacks                   | Stored attacks are those where the injected script is permanently stored on the target servers, such as in a database, in a message forum, visitor log, comment field, etc. |
| Reflected XSS Attacks                | Reflected attacks are those where the injected script is reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request. |
| Carriage Return Line Feed (CRLF)     | A CRLF Injection attack occurs when a user manages to submit a CRLF into an application. This is most commonly done by modifying an HTTP parameter or URL. |
| Content Security Policy (CSP)        | CSP specification use “directive” where a directive defines a loading behavior for a target resource type. |
| Cross Origin Resource Sharing (CORS) | Cross Origin Resource Sharing (CORS) is a mechanism that enables a web browser to perform cross-domain requests using the XMLHttpRequest (XHR) Level 2 (L2) API in a controlled manner. |


# Vulnerability Classifications

For this report, vulnerability severities are classified and measured using the [Bugcrowd’s Vulnerability Rating](https://bugcrowd.com/vulnerability-rating-taxonomy) system.

### P1 - Critical

Vulnerabilities that cause a privilege escalation on the platform from unprivileged to admin, allows remote code execution, financial theft, etc. Examples: vulnerabilities that result in Remote Code Execution such as Vertical Authentication bypass, SSRF, XXE, SQL Injection, User authentication bypass.

### P2 - High Risk

Vulnerabilities that affect the security of the platform including the processes it supports. Examples: Lateral authentication bypass, Stored XSS, some CSRF depending on impact.

### P3 - Medium Risk

Vulnerabilities that affect multiple users, and require little or no user interaction to trigger. Examples: Reflective XSS, Direct object reference, URL Redirect, some CSRF depending on impact.

### P4 - Low Risk

Issues that affect singular users and require interaction or significant prerequisites (MitM) to trigger. Examples: Common flaws, Debug information, Mixed Content.

### P5 - Acceptable

Non-exploitable weaknesses and “won’t fix” vulnerabilities. Examples: Best practices, mitigations, issues that are by design or acceptable business risk to the customer such as use of CAPTCHAS.

# Executive Summary

QuoccaBank is a "Cyber-Friendly" bank with the prospects of being a reliable and secure service for users. Our team has been in charge of conducting preliminary security assessments on the QuoccaBank system and infrastructure. QuoccaBank has asked us for an interim document detailing our findings and assessment of security vulnerabilities currently present in the system. The main goals of the report are to

- identify discovered vulnerabilities,
- showcase the proof of concept,
- explaining the impacts such vulnerabilities may have,
- providing some remediations to patch the vulnerability, and
- CORS testing and detailing Same Site impacts.

The scope of the report includes the following subdomains:

- report.quoccabank.com
- csp.quoccabank.com
- profile.quoccabank.com
- science-today.quoccabank.com
- sturec.quoccabank.com
- support-v2.quoccabank.com
- wallet.quoccabank.com
- ctfproxy2.quoccabank.com

The vulnerabilities discussed have been rated according to [Bugcrowd’s Vulnerability Rating](https://bugcrowd.com/vulnerability-rating-taxonomy) system where the severity is measured on a scale from P1 - Critical to P5 - Acceptable.

# Summary of Results

After conducting thorough testing on QuoccaBank's systems and infrastructure, our team has discovered that there exist 1 vulnerabilities classified under P1 - Critical, 6 vulnerabilities classified under P2 - High Risk, 7 vulnerabilities classified under P3 - Medium Risk, 2 vulnerabilities classified under P4 - Low Risk and 4 vulnerabilities classified under P5 - Acceptable. An entire list of vulnerabilities can be found on the table of contents.

