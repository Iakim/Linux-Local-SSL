# Add a local certificate to apache


#### Step 1

      openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365

#### Step 2

      NameVirtualHost *:80
      <VirtualHost *:80>
        ServerName aplication.domain.com
       DocumentRoot /var/www/html/aplication
        Redirect /secure https://aplication.domain.com
      </VirtualHost>

      <VirtualHost *:443>
        SSLEngine on
        SSLCertificateFile /etc/pki/tls/certs/cert.pem
        SSLCertificateKeyFile /etc/pki/tls/private/key.pem
        <Directory /var/www/html/aplication>
        AllowOverride All
        </Directory>
        DocumentRoot /var/www/html/aplication
        ServerName aplication.domain.com
      </VirtualHost>
      
#### Step 3

      cp key.pem /etc/pki/tls/private/
      cp cert.pem /etc/pki/tls/certs/
      
#### Step 4

      service httpd restart
