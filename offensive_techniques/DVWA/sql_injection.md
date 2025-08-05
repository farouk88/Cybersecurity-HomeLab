````markdown
# SQL Injection Attack

## Description
Exploited SQL injection vulnerability to bypass authentication and extract sensitive data.

## Example Payload
```sql
1' OR '1'='1
````

## Outcome

* Retrieved all users' data from the database.
* Bypassed login authentication.

````