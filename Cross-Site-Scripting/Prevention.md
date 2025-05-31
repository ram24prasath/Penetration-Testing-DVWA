# Prevention Techniques against XSS type of Vulnerabilities

XSS attacks are serious and can lead to account impersonation, observing user behavior, stealing sensitive data, session hijacking.

In order for an XSS attack to be successful, an atatcker must be able to insert and execute malicous content in a webpage.

This type of attack is possible when an application takes input from the user and uses this input as a variable as a part of web application without any validation.


Cross-site scripting prevention can be layered via two layers of defence:

- Validate input on arrival.
- Encode data on output.

## Encode Data on arrival

Encoding should be applied directly before user-controlled data is written to a page.

Example of encoding:

  - `<` encoded to: `&lt;`
  - `>` encoded to: `&gt;`

## Validate input on arrival

Input validation should ideally work by blocking invalid inputs. Alternate clean approach to this would be creating a white list that contains valid set of input that the application accepts.

- Validating that input contains only an expected set of characters. 

### Escaping and encoding

- Escaping and encoding are defensive Security mechanisms that allow organisations to prevent injection attacks.
- CSS escape, HTML escape, Javascript escape and URL escape.

### Use HTML sanitizers

User inputs that needs to contain HTML codes, cannot be escaped, in this case use appropiate and trusted sanitizers to clean and parse HTML.

### Set HTTPOnly

Setting HTTP flag for cookies, means that it cannot be accessed at the client-side JavaScript.

### Use Content Security Policy

CSP response header in HTTP, enables users to dynamically allocate resources based on request source.

Content security policy (CSP) is the last line of defense against cross-site scripting. If your XSS prevention fails, you can use CSP to mitigate XSS by restricting what an attacker can do. 

Policy specifies that resources such as images and scripts can only be loaded from the same origin as the main page.


Below cheat sheet can be used to test against XSS type of Attacks.

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet



