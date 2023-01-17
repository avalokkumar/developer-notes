### Creating a self signed certificate in local machine

You can create a self-signed certificate on a Mac local machine using the openssl command line tool. Here are the steps to create a self-signed certificate and associate it to a particular domain name:

* Open the Terminal on your Mac and run the following command to create a private key:</br>
`openssl genrsa -out example.com.key 2048`

> This will create a private key file named "example.com.key" in the current directory.

* Next, use the private key to create a certificate signing request (CSR) file:</br>
`openssl req -new -key example.com.key -out example.com.csr`

> This command will prompt you for various information such as the country, state, organization, and the common name (CN) which should be the domain name you are associating the certificate with (e.g. example.com).

* Use the CSR file to create a self-signed certificate:</br>
`openssl x509 -req -days 365 -in example.com.csr -signkey example.com.key -out example.com.crt`

> This command will create a self-signed certificate named "example.com.crt" in the current directory, valid for 365 days.

Now that you have the certificate file and key, you can use them to configure your web server, load balancer, or other service that requires an SSL/TLS certificate.
It's worth noting that as a self-signed certificate is not trusted by web browsers and other clients, it will generate a security warning message when trying to access the website. If you want to avoid this warning message you should use a trusted certificate from a certificate authority (CA) such as DigiCert, GlobalSign, or Let's Encrypt.


---
### PEM, CRT, and KEY files

#### PEM, CRT, and KEY files are all used in the context of SSL/TLS certificates, which are used to establish secure connections between web servers and clients.

#### PEM (Privacy Enhanced Mail) files are the most common format for SSL/TLS certificates and are used to store the certificate, private key, and any intermediate CA certificates. </br>PEM files are encoded in base64 and typically have a .pem, .crt, .cer, or .key file extension. A PEM file can contain multiple items, for example a certificate and a private key.

> Here's an example of a PEM file containing a certificate:

```
-----BEGIN CERTIFICATE-----
MIIEkjCCA3qgAwIBAgIQCgFBQgAAAVOFc2oLheynCDANBgkqhkiG9w0BAQsFADA/
MSQwIgYDVQQKExtEaWdpdGFsIFNpZ25hdHVyZSBUcnVzdCBDby4xFzAVBgNVBAMT
DkRTVCBSb290IENBIFgzMB4XDTE2MDMxNzE2NDA0NloXDTIxMDMxNzE2NDA0Nlow
SjELMAkGA1UEBhMCVVMxFjAUBgNVBAoTDUxldCdzIEVuY3J5cHQxIzAhBgNVBAMT
GkxldCdzIEVuY3J5cHQgQXV0aG9yaXR5IFgzMIIBIjANBgkqhkiG9w0BAQEFAAOC
AQ8AMIIBCgKCAQEAnNMM8FrlLke3cl03g7NoYzDq1zUmGSXhvb418XCSL7e4S0EF
q6meNQhY7LEqxGiHC6PjdeTm86dicbp5gWAf15Gan/PQeGdxyGkOlZHP/uaZ6WA8
SMx+yk13EiSdRxta67nsHjcAHJyse6cF6s5K671B5TaYucv9bTyWaN8jKkKQDIZ0
Z8h/pZq4UmEUEz9l6YKHy9v6Dlb2honzhT+Xhq+w3Brvaw2VFn3EK6BlspkENnWA
a6xK8xuQSXgvopZPKiAlKQTGdMDQMc2PMTiVFrqoM7hD8bEfwzB/onkxEz0tNvjj
/PIzark5McWvxI0NHWQWM6r6hCm21AvA2H3DkwIDAQABo4IBfTCCAXkwEgYDVR0T
AQH/BAgwBgEB/wIBADAOBgNVHQ8BAf8EBAMCAYYwfwYIKwYBBQUHAQEEczBxMDIG
CCsGAQUFBzABhiZodHRwOi8vaXNyZy50cnVzdGlkLm9jc
```

#### CRT (Certificate) files are similar to PEM files and also contain the SSL/TLS certificate. The main difference is that CRT files are typically in the DER format, which is a binary format as opposed to the base64-encoded PEM format. CRT files have a .crt or .cer file extension.

> Here's an example of a command to convert a PEM file to a CRT file:

```
openssl x509 -outform der -in certificate.pem -out certificate.crt
```

#### KEY (Private Key) files contain the private key associated with an SSL/TLS certificate. They are used in combination with the certificate and any intermediate CA certificates to establish a secure connection. KEY files are typically in the PEM format and have a .key file extension.

> Here's an example of a command to generate a private key file:

```
openssl genpkey -algorithm RSA -out private_key.key
```
