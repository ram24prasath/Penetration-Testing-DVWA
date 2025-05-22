# Brute Force Vulnerability 

Brute force vulnerability occurs in an application, when the application fails to limit or provide protection against repeated attempt to guess credentials.

This vulnerability can be exploited by the attacker to try all possible combinations of the credentials which can lead to unauthorized access to the application.

## Brute Forcing into DVWA in Low Security Level

We are using burp suite to capture request sent to the application, using Intercept function iin burp suite, we can different attack types to brute force into the application by using payload
from the seclists.

![image](https://github.com/user-attachments/assets/8fd11944-73d8-493d-8ed0-d89ab98f51b5)

Make sure to turn on Intercept in burp suite before submittting the credentials. Intially use username: `admin` and password: `test`.

Here is the intercepted request in burp suite:

![image](https://github.com/user-attachments/assets/1ec892d0-2d11-43fa-8ae0-ad5999ca5ff9)

Send the captured request to Intruder and navigate to intruder tab in burp suite.

1. In postion tab: select the password `test` and click on ![image](https://github.com/user-attachments/assets/0bc23f95-2f25-4f91-bbcf-bd1de80b0222).
2. In Payload tab:
     Select Payload Type: `Simple List`
     In playload configuration, load paylaod file from `/usr/share/seclists/Passwords/Common-Credentials/`.
3. Click on start attack. ![image](https://github.com/user-attachments/assets/2a619d4b-c8cf-4178-b1cb-849fecd353d1)


After the attack is finished, sort the response by length. Observe the response for the top request. Our atatck has successfully brute forced into login to application.

![image](https://github.com/user-attachments/assets/febc5429-1343-45c5-a57b-8ffb7253083f)

## Brute Forcing into DVWA in Medium Security Level

Repeat the same process, but set security level to medium.

![image](https://github.com/user-attachments/assets/f55391b6-3144-4696-8e18-2fe5e94d4215)

The result is the same but this time it takes longer for the burp suite to complete the atatck.
