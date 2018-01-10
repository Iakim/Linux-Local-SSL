# Add a local certificate to apache


#### 1 step

      openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
