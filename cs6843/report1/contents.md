## Vulnerability Classification

- LOW
- MEDIUM
- HIGH
- CRITICAL

## Subdomains Vulnerabilities

- letters.quoccabank.com
  - CRITICAL: Command Injection via LaTeX
- signin.quoccabank.com
  - CRITICAL: SQL Injection through DNS Record
- blog.quoccabank.com
  - LOW: Sensitive Metadata in Page Source
  - HIGH: Weak Passwords and Error Messages
  - LOW: Default Configurations: Login Page is accessible
  - MEDIUM: IDOR through URL Parameters
- bfd.quoccabank.com
  - CRITICAL: Local file inclusion on 'bfd.quoccabank.com'
- v[1234].feedifier.quoccabank.com
  - CRITICAL: XML external entities vulnerability in 'feedifier.quoccabank.com' leading to local file inclusion
- gcc.quoccabank.com
  - HIGH: Partial local file inclusion and stored xss on 'gcc.quoccabank.com' leading to possible Remote code execution
- notes.quoccabank.com
  - HIGH: Unverified JWT token on 'notes.quoccabank.com' leads to vertical privilege escalation
- support.quoccabank.com
  - MEDIUM: Insecure direct object reference vulnerability in 'support.quoccabank.com' leads to unauthorized access and information leakage.
- sales.quoccabank.com
  - CRITICAL: Clientside Session Validation via Cookies
- pay-portal.quoccabank.com
  - CRITICAL: SQL Injection in `period` parameter
- bigapp.quoccabank.com
  - CRITICAL: SQL Injection in Login Parameters
  - HIGH: SQL Injection in Registration Page
  - LOW: No Distinction Between GET and POST Methods in Login Endpoint
  - CRITICAL: SQL Injection in REST API
  - HIGH: Insecure Hash Algorithm for User Credentials
  - CRITICAL: Clientside Session Validation via Cookies
- files.quoccabank.com
  - CRITICAL: IDOR vulnerability in files.quoccabank.com
  - HIGH: XSS in files.quoccabank.com
  - CRITICAL: Insecure authentication in files.quoccabank.com/admin
  - CRITICAL: Vertical privilege escalation and logging in as any user in files.quoccabank.com

## Recon Vulnerabilities

blog.quoccabank.com

- LOW: Sensitive Metadata in Page Source
- LOW: Default Configurations: Login Page is accessible

## Authentication and User Access Vulnerabilities

**Authentication**

bigapp.quoccabank.com

- LOW: No Distinction Between GET and POST Methods in Login Endpoint

blog.quoccabank.com

- HIGH: Weak Passwords and Error Messages

notes.quoccabank.com

- HIGH: Unverified JWT token on 'notes.quoccabank.com' leads to vertical privilege escalation

bigapp.quoccabank.com

- HIGH: Insecure Hash Algorithm for User Credentials

files.quoccabank.com

- CRITICAL: Insecure authentication in files.quoccabank.com/admin
- CRITICAL: Vertical privilege escalation and logging in as any user in files.quoccabank.com

**Session Management**

bigapp.quoccabank.com

- CRITICAL: Clientside Session Validation via Cookies

sales.quoccabank.com

- CRITICAL: Clientside Session Validation via Cookies

## Injection & Server-side vulnerabilities

**IDOR**

support.quoccabank.com

- MEDIUM: Insecure direct object reference vulnerability in 'support.quoccabank.com' leads to unauthorized access and information leakage.

blog.quoccabank.com

- MEDIUM: IDOR through URL Parameters

files.quoccabank.com

- CRITICAL: IDOR vulnerability in files.quoccabank.com

**SQL Injection**

bigapp.quoccabank.com

- HIGH: SQL Injection in Registration Page

pay-portal.quoccabank.com

- CRITICAL: SQL Injection in `period` parameter

signin.quoccabank.com

- CRITICAL: SQL Injection through DNS Record
- CRITICAL: SQL Injection to Change Passwords

bigapp.quoccabank.com

- CRITICAL: SQL Injection in Login Parameters
- CRITICAL: SQL Injection in REST API

**Local File Inclusion**

gcc.quoccabank.com

- HIGH: Partial local file inclusion and stored xss on 'gcc.quoccabank.com' leading to possible Remote code execution

v[1234].feedifier.quoccabank.com

- CRITICAL: XML external entities vulnerability in 'feedifier.quoccabank.com' leading to local file inclusion

bfd.quoccabank.com

- CRITICAL: Local file inclusion on 'bfd.quoccabank.com'

**Command Injection**

letters.quoccabank.com

- CRITICAL: Command Injection via LaTeX

## Client-Side

files.quoccabank.com

- HIGH: XSS in files.quoccabank.com

