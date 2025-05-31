# Prevention Techniques against SQLi

## 1. Use Prepared statements and parameterized Queries

Prepared statements and parameterized queries ensure that the user inputs are treated as data rather than part of SQL query.

- Parameterized queries for the developers to define all SQL codes first and pass in each parameters to the query later.
- Prepared statement ensures that an attacker cannot change the intent of the SQL statement.

## 2. Use properly constructed stored procedures

Stored procedures are pre-defined SQL queries stored in database. These procedures can help prevent SQL injection because they don't dynamically construct sql queries.

```bash
CREATE PROCEDURE GetUserByUsername (IN username VARCHAR(50))
BEGIN
   SELECT * FROM users WHERE username = username;
END;
```

The difference between prepared statements and stored procedures is that the SQL code for a stored procedure is defined and stored in the database itself, then called from the application. 

## 3. Allow-list Input Validation

Ensure that user inputs are validated before being used in SQL queries. Only allow certain characters and patterns, such as alphanumeric input, for fields like usernames or email addresses.
  
## 4. Use ORM frameworks

ORM framework can help prevent SQL injection by automatically handling query generation, preventing dynamic query construction.

