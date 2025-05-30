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



