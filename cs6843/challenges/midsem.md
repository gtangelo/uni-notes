# Midsem Challenges

### midsem1.quoccabank.com

- COMP6443MIDSEM{Q1_HTML.ejUzMTI3OTk=.CWsNQvQVtWVro3cJrBwiRg==}

  - check source code

- COMP6443MIDSEM{Q1_HEADER.ejUzMTI3OTk=.hec+R9ZcWXjXE7LZjXtjpQ==}

  - Checking the cookie gives us `false:68934a3e9455fa72420237eb05902327`. Looking up what the hash `68934a3e9455fa72420237eb05902327` is, it appears to be a MD5 of `false`. So the cookie is in the format of `<bool>:MD5<bool>`.
  - Changing to become true, `true:b326b5062b2f0e69046810717534cb09` and checking the response header gives us the flag.

- COMP6443MIDSEM{Q1_ROBOTS.ejUzMTI3OTk=.Y5kkv377YSyQ7TMcisZdmA==}

  - Checking robots.txt, it would appear that a route exist called `/quack` and is only accessible with the `User-agent: Quoccrome`. Using burp to manipulate the request, we get the flag.

### midsem2.quoccabank.com

- COMP6443MIDSEM{Q2.ejUzMTI3OTk=.DMMqx3Zv0fkdipqEudJT4w==}
  - Using burp, change the POST request to have a fee of the item that you have enough coins to purchase.

### midsem3.quoccabank.com

- COMP6443MIDSEM{Q3.ejUzMTI3OTk=.XSyqjFBeYcl8Yl+ZKSE9/w==}
  - Inspecting `/robots.txt`, we are given a route called `/super-secret-backup.zip`. Accessing that route gives us a piece of source code which tells us that the password is the MD5 of the username
  - Using repeater, since the page automatically reloads once logged in, sending a POST request with username `admin` and password `21232f297a57a5a743894a0e4a801fc3` gives us the flag.

### midsem4.quoccabank.com

- COMP6443MIDSEM{Q4.ejUzMTI3OTk=.OCaF6aa/LhnGHg0WOndh9w==}
  - Using the username `admin` and password `admin`, we are brought to a 2FA screen. However, it appears that out input for the code is being verified by an API on the route `/api/verify_code/<code>`. The payload tells which digit is wrong. We can now guess and check the verification code which is `820594`

### midsem5.quoccabank.com

- COMP6443MIDSEM{Q5_IDOR.ejUzMTI3OTk=.T5JZ5TglA07RI+X7kxEWIQ==}

  - It would appear that when creating a ticket, it is base64 encoded three times. Also, it appears that it is using the ticket number in the url `/raw/<ticket number base64 3 times>`
  - Accessing ticket number `2` gives us the flag

- COMP6443MIDSEM{Q5_2ND_POST.ejUzMTI3OTk=.mped61cTmUacEVE1s1JShA==} 

  - Accessing ticket number `3` gives us a suspicious error code 403 with the message `Have you tried being a better hacker???` which is different to the other error messages for invalid tickets.
  - It seems like that the backend could perform an SQL query with the base64 encoded ticket number. We can inject the SQLi payload `' or id='3' -- ` so that we can grab the ticket which contains the flag

- COMP6443MIDSEM{Q5_3RD_POST.ejUzMTI3OTk=.TyLFZiHRzy2WmnXBTxqA5w==}

  - Knowing that it is SQLi, we can perhaps extract more information using the script below to extract the row in the database with the flag

    ```python3
    if __name__ == '__main__':
        for row in range(700):
            # i = "' OR id='3' -- )"
    
            # ~ around row 630
            # i = f"' UNION (SELECT table_name, column_name FROM information_schema.columns LIMIT 1 OFFSET {row})  -- )"
            
            i = f"' UNION (SELECT id, contents FROM supersecret LIMIT 1 OFFSET {row})  -- )"
            i_1 = base64.b64encode(i.encode('ascii'))
            i_2 = base64.b64encode(i_1)
            i_3 = base64.b64encode(i_2)
            brute_force(i_3.decode())
    ```

    
