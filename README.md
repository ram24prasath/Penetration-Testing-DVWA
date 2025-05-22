# Web-Application-Pen-Testing

# Penetration Testing Project - DVWA Web Application

This repository contains the work related to my penetration testing project, where I will be testing the security of the DVWA (Damn Vulnerable Web Application). DVWA is a web application designed for security professionals and penetration testers to practice and learn about web application vulnerabilities.

## Overview

The objective of this project is to identify, exploit, and document common web vulnerabilities in DVWA. The project will focus on different security issues such as SQL injection, Cross-Site Scripting (XSS), Command Injection, and more.

DVWA provides a vulnerable environment where users can perform penetration tests in a controlled environment. The web application can be configured to different levels of difficulty (Low, Medium, High, and Impossible), and this project will explore vulnerabilities at different security levels.

## Project Goals

- Identify common vulnerabilities within the DVWA web application.
- Learn about the exploitation techniques for each vulnerability.
- Document findings, and suggest mitigations for each vulnerability.
- Develop a comprehensive report based on the testing outcomes.

## Tools Used

The following tools will be used during the penetration testing process:

- **Burp Suite** - Intercepting proxy for scanning and manipulating web requests.
- **OWASP ZAP** - Another powerful security scanner and proxy tool.
- **SQLmap** - Automated tool for detecting and exploiting SQL injection flaws.
- **Nikto** - Web server scanner for finding potential vulnerabilities.
- **Hydra** - Brute-force tool for testing password strength.

## Testing Scope

The scope of this penetration test includes testing various aspects of the DVWA application, including but not limited to:

- **SQL Injection**
- **Cross-Site Scripting (XSS)**
- **Command Injection**
- **File Upload Vulnerabilities**
- **Insecure Direct Object References (IDOR)**
- **Cross-Site Request Forgery (CSRF)**
- **Security Misconfigurations**

## Installation and Setup

To begin testing DVWA, please follow these steps to set up your local environment:

1. **Install Docker and DVWA** (if not already installed):

   Follow the instructions to setup docker and DVWA through [Installation Setup](https://github.com/ram24prasath/Web-Application-Pen-Testing/blob/main/DVWA_Setup.md).
   
2. **Start the DVWA Docker container**:

   ```bash
   docker-compose up -d
3. **Access DVWA**:
   Open a browser and go to http://localhost:4280. The default credentials are:

    Username: admin

    Password: password

4. Configure DVWA Security level after logging in to the application.
  After logging in, navigate to the "DVWA Security" page and set the security level to the desired difficulty (Low, Medium, High, or Impossible).

## Disclaimer

This project is for educational purpose. 
Feel free ontribute additional resources or documentation to this project. 
