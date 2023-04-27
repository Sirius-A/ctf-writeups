# Authentication vulnerabilities

## Username enumeration via different responses

Use Intruder with username and pw as sniper targets

## 2FA simple bypass

1. Login as `wiener:peter`
1. Use portswigger e-mail to login with 2FA
1. capture e-mail change request into repeater
1. logout
1. login as `carlos:montoya`
1. copy session token from the new session
1. insert session token in the prev. captured request to change the e-mail
1. insert wrong code and login again as carlos
1. recieve 2FA code via e-mail
1. ???
1. Profit
