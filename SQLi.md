# SQL Injection

Objective: DVWA has 5 users in the database with ID's from 1 to 5. Retrieve information via SQLi.

## Security Level: LOW

DVWA has the function, where user can enter ID and the application retreives First name and Surname that belongs to the ID.

![image](https://github.com/user-attachments/assets/005092a9-d8cf-4a4c-ba74-a35df6a30880)

The function uses the below SQL query to retrieve data from the data base:

```bash
SELECT first_name, last_name FROM users WHERE user_id = '$id';
```

Since there is no input validation, sql injection can be exploited. Passing single qoute as input return internal server error, indicates sqli is 
possible.

Using input as below.
```
1' OR '1'='1
```
This input is passed to the SQL statement as below:
```
SELECT first_name, last_name FROM users WHERE user_id = '1' OR '1' = '1';
```
Since '1' = '1' is always true, select statement returns all the values present in the database.

![image](https://github.com/user-attachments/assets/0c4da4b5-a72d-47da-8109-15b00490db87)

---

## Retrieve Password from another table using UNION attack

First, we need find number of columns present in the `user` table. We can confirm this by passing the following crafted input.

- `' order by 1#` - causes fatal error
- `' order by 2#` - No error
- `' order by 3#` - fatal error

This confirms that there are 2 columns.

Next, we need to find datatype of the columns.

- `' UNION SELECT 'abc','abc' from users #`

From MariaDB knowledge base, we can figure out the column names.

https://mariadb.com/kb/en/mysql-user-table/

Now, use the found column names (user, password) in the union sql injection

```
' UNION SELECT user, password from users #

```

Query returned username and password hashes.

![image](https://github.com/user-attachments/assets/a6ce6916-997a-4980-8cf1-54ac567905fc)

Lets try this burp suite:

Request from the application is intercepted and sent to repeater.

In the request tab, Used `' UNION SELECT user, password from users #` and url encoded and sent to the application.

![image](https://github.com/user-attachments/assets/b7e726d3-8571-43ab-8fc3-cc4415bbb7d1)

The response received:

![image](https://github.com/user-attachments/assets/d7ef67f5-55c8-45d1-a9b5-6438c2934162)


The hashed password can be decoded.


## Security Level: Medium

