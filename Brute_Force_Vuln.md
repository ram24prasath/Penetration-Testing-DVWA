# Brute Force Vulnerability 

Brute force vulnerability occurs in an application, when the application fails to limit or provide protection against repeated attempt to guess credentials.

This vulnerability can be exploited by the attacker to try all possible combinations of the credentials which can lead to unauthorized access to the application.

## Brute Forcing into DVWA in Low Security Level

We are using burp suite to capture request sent to the application, using Intercept function iin burp suite, we can different attack types to brute force into the application by using payload
from the seclists.

![image](https://github.com/user-attachments/assets/2acf43e5-fac9-403b-8cbe-943d0e00e761)


Make sure to turn on Intercept in burp suite before submittting the credentials. Intially use username: `test` and password: `test`.

Here is the intercepted request in burp suite:

![image](https://github.com/user-attachments/assets/e6b0fabd-e77f-4719-a4a1-3ac670a77498)


Send the captured request to Intruder and navigate to intruder tab in burp suite and follow the steps below:

1. Select Brute force attack type: `Cluster Bomb attack`. Since we want to enumerate username and password. If we already know username and we want to brute force only password then select atatck type `Sniper attack`.
   ![image](https://github.com/user-attachments/assets/0a39522e-c56c-4a36-867d-a286b2f679d9)

2. In the position tab, add payload symbol to the username and password in the request.
   ![image](https://github.com/user-attachments/assets/4fede124-b606-49d1-8882-015968e99149)

3. In the payload tab, Select paylaod position 1 and paylaod type `simple list`. In payload configuration load file for **username** enumeration from /usr/share/seclists/Usernames/top-usernames-shortlist.txt.
   
4. Select paylaod position 1 and paylaod type `simple list`. In payload configuration load file for **password** enumeration from /usr/share/seclists/Passwords/Common-Credentials/10-million-password-list-top-100.txt
   
5. Start the attack.


After the attack is finished, sort the response by length. Observe the response for the top request. Our atatck has successfully brute forced into login to application.

![image](https://github.com/user-attachments/assets/0fbbb8b7-bb52-45b8-a00b-4f745e49d912)

Brute Force was successful, can be verified from the response tab. 

```bash
Username: admin
Password: password
```

## Brute Forcing into DVWA in Medium Security Level

Repeat the same process, but set security level to medium.

![image](https://github.com/user-attachments/assets/f55391b6-3144-4696-8e18-2fe5e94d4215)

The result is the same but this time it takes longer for the burp suite to complete the atatck.
