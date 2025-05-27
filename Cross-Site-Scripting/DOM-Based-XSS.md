# DOM based XSS

XSS attack wherein the attack payload is executed as a result of modifying DOM in victim's browser used by the client side script.

DOM-based XSS vulnerabilities usually arise when JavaScript takes data from an attacker-controllable source, such as the URL, and passes it to a sink that supports dynamic code execution, such as eval() or innerHTML. 

To deliver a DOM-based XSS attack, you need to place data into a source so that it is propagated to a sink and causes execution of arbitrary JavaScript. 

The most common source for DOM XSS is the URL, which is typically accessed with the window.location object. 

## Security Level: Low

We figured that DOM-based XSS atatck is commonly carried out through URL.

![image](https://github.com/user-attachments/assets/d9ad6854-0d44-4376-96ac-8e072b94fd1d)

When we select a language and submit, the url of the application is as follows:

`http://localhost:4280/vulnerabilities/xss_d/?default=Spanish`

If we can craft the url to inject script, we can successfully carry out DOM-based XSS.

`http://localhost:4280/vulnerabilities/xss_d/?default=<script>alert(document.cookie)</script>`

![image](https://github.com/user-attachments/assets/34ba75d9-9099-4949-acb9-decbba7aa853)

## Security Level: Medium


The developer has tried to add a simple pattern matching to remove any references to "<script" to disable any JavaScript. 

```bash
    # Do not allow script tags
    if (stripos ($default, "<script") !== false) {
        header ("location: ?default=English");
        exit;
```

Since, the <script> tag will be removed by the javascript, previous level injection will not work at this level.

instead we can use `<img src/onerror=alert(document.cookie)>`

Crafted URL looks like this:
`http://localhost:4280/vulnerabilities/xss_d/?default=English>/option></select><img src/onerror=alert(document.cookie)>`

![image](https://github.com/user-attachments/assets/b777a06e-ba01-42e4-85b0-2ec588903e56)

## Security Level: High

In this level, instead removing only particular script tags, developers create a allow list of valid tags in url, and block all others.

``` bash
    # White list the allowable languages
    switch ($_GET['default']) {
        case "French":
        case "English":
        case "German":
        case "Spanish":
            # ok
            break;
        default:
            header ("location: ?default=English");
            exit;
```

The technique to avoid sending the payload to the server hinges on the fact that URI fragments (the part in the URI after the “#”) is not sent to the server by the browser. Thus, any client side code that references, say, document.location, may be vulnerable to an attack which uses fragments, and in such case the payload is never sent to the server. For example, the above DOM based XSS can be modified into:

`http://localhost:4280/vulnerabilities/xss_d/?#default=English<script>alert(document.cookie)</script>`

---
