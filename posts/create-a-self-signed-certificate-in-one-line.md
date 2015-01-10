<!-- 
.. title: Create a self-signed certificate in one line
.. slug: create-a-self-signed-certificate-in-one-line
.. date: 02/01/2014 00:00:00 AM UTC+02:00
.. tags: web, openssl
.. link: 
.. description: 
.. type: text
-->

```console
$ openssl req -nodes -x509 -newkey rsa:4096 -sha512 -days 365 -keyout cert.key -out cert.pem
```

Let's analyze this command:

* `req`: request a new PKCS#10 certificate;
* `-nodes`: do not encrypt the private key (no password);
* `-x509`: output a self-signed certificate instead of a certificate request;
* `-newkey rsa:4096`: create a new certificate request and a new 4096 bits RSA key;
* `-sha512`: sign the request with a SHA-512 message digest;
* `-days 365`: the certificate will be valid for 365 days;
* `-keyout cert.key`: private key filename;
* `-out cert.pem`: output filename.

