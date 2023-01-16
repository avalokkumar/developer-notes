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
