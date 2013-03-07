# tornado_apns

A Python library for interacting with the Apple Push Notification service 
(APNs) for tornado async programming

## Sample usage

```python
from apns import APNs, Payload
from tornado import ioloop

apns = APNs(use_sandbox=True, cert_file='cert.pem', key_file='key.pem')

def success():
    print("Sent push message to APNS gateway.")
    ioloop.IOLoop.instance().stop()

def send():
    payload = Payload(alert="Hello World!", sound="default", badge=1)
    apns.gateway_server.send_notification(options.push_token, payload, success)

# Send a notification
token_hex = 'b5bb9d8014a0f9b1d61e21e796d78dccdf1352f23cd32812f4850b87'
apns.gateway_server.connect(send)

ioloop.IOLoop.instance().start()
```

For more complicated alerts including custom buttons etc, use the PayloadAlert 
class. Example:

```python
alert = PayloadAlert("Hello world!", action_loc_key="Click me")
payload = Payload(alert=alert, sound="default")
```

To send custom payload arguments, pass a dictionary to the custom kwarg
of the Payload constructor.

```python
payload = Payload(alert="Hello World!", custom={'sekrit_number':123})
```

## Further Info

[iOS Reference Library: Local and Push Notification Programming Guide][a1]

## Credits

Written and maintained by Simon Whitaker at [Goo Software Ltd][goo].

[a1]:http://developer.apple.com/iphone/library/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008194-CH1-SW1
[goo]:http://www.goosoftware.co.uk/
