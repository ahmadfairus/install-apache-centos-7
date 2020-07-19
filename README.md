##### step by step install apache (httpd) on centos 7

##### Install Package Apache
yum install httpd -y
systemctl enable httpd
service httpd start

##### create folder for place of configuration
mkdir -p /etc/httpd/conf.d/vhost

##### this line to the end of file /etc/httpd/conf/httpd.conf
IncludeOptional conf.d/vhost/*.conf

##### crate new file configuration 
vim /etc/httpd/conf.d/vhost/www.testing.com.conf

##### type this configuration

    <VirtualHost *:80>

        ServerName testing.com
        DocumentRoot /data/www/testing.com
        
        CustomLog /data/www/logs/testing.com-access.log combined
        ErrorLog /data/www/logs/testing.com-error.log
        
        <Directory "/data/www/testing.com">
                Options -Indexes -MultiViews -FollowSymlinks +SymLinksIfOwnerMatch
                AllowOverride all
                Require all granted
        </Directory>
        
    </VirtualHost>

##### make example application with html and make log location
    mkdir -p /data/www/testing.com
    mkdir -p /data/www/logs
    vim /data/www/testing.com/index.html
##### type this code and save
    <html>
      <body>
        Test Apache
      </body>
    </html>

##### confim configuration with command
httpd -t

##### Restart Apache service
service httpd restart

