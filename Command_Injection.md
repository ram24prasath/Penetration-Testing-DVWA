# Command Injection

Command injection is an attack in which the goal is execution of arbitrary commands on the host operating system via a vulnerable application. 

Command injection attacks are possible when an application passes unsafe user supplied data (forms, cookies, HTTP headers etc.) to a system shell.

In this attack, the attacker-supplied operating system commands are usually executed with the privileges of the vulnerable application. 
Command injection attacks are possible largely due to insufficient input validation.

## Security Level: Low

We have a form field that takes input from user(intended for ip address), from the page source we can see that the application pings the ip address four times.

![image](https://github.com/user-attachments/assets/167d96cf-6846-4aa5-9c67-ac28abae7521)

Intended use of this part is to ping a device through the webserver. Upon user entering the IP address in the input form, it executes the following command in the server.

` ping -c 4 127.0.0.1 `

Here command injection would be possible if the atatcker can escape out of the designed command and executed unintentional actions by crafted the input such as.

` 127.0.0.1 & whoami`

What this input does is, it pings the ip address given additionally it retrieves information about the current user through the command `whoami`.



