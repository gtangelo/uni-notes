# Revision

- 
- bug bounty cheat sheets
- Automated tooling:
  - dirb, dirbuster, gobuster (have a wordlist ready)
  - burp passive scanner
  - fingerprint / check for CVE’s (whatweb, etc)
  - altdns, zdns, massdns
- 



Tips before starting any challenges:

- view source code
- HTML comments, JS files, resources that has been included in the html file (i.e. CSS)
- HTTP headers
- cookies
- CSP
- robots.txt



Authentication: identifies a specific user logging in

- Typical attacks
  - Brute force / simple passwords (e.g. `admin:admin` or `admin:password`)
  - Injection attacks against login functionality
  - Broken forgot password functionality
  - Register page looking for enumerating usernames
  - XSS (stealing a user’s cookie)
  - Session fixation (forcibly set a user’s cookie).

Authorization: identifies whether a user is permitted to take an action or use a resource.

- Typical attacks
  - IDOR (id=2)
  - Browse to privileged pages / content as unprivileged user i.e. `/admin`
  - Modify own user pages
  - CSRF (force someone else to take a privileged action)
  - XSS (use another user to fetch privileged content)

Server-Side Attacks:

- Magic string: 

  ```
  ‘”;<lol/>../--#`ls`
  ```

- URL Encodings - check burp

SQLi:

- Quote styles (single vs double quote)
- Comment styles (--, #, ;)
- Wildcards (%, *)
- Binary searches vs delays - i.e. if character is m, then delay

Command Injection:

- `ping 8.8.8.8 && dd if=/dev/urandom of=/dev/sda1 bs=1 count=1024`
- Be aware of OS specifics
  - Chaining commands
  - UNC paths
  - Backticks
- Cheatsheet: https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html

Topic 4:

- CSRF
- Same Origin Policy: JavaScript from one origin cannot access data from another origin.

XSS:

- DONT use alert1 - use alert 2 since it may be blocked



Revision:

- owasp juice shop
- ctf challenges
- ctftime.org
- pico ctf
- buggy webapp
- web goat
- hackthebox
- ctf101



9.25



do readings at the end of the lecture



- set up flag alert
- copy as request extension burp
- clonse word list to /var/wordlists
- burp passive scaner -> target> sitemap (change scope)
- fingerprinting - whatweb i.e. type this in shell `whatweb https://quoccabank.com` - identify web server it is running
  - fingerprinting is a technique
- 





