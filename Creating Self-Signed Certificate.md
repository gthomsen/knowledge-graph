Tags: #openssl #software-engineering 

For when you need a self-signed certificate that can be trusted:
```shell
# creates a 4096-bit key valid for the next year.
$ openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
```