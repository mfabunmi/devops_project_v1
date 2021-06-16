# Project 2

1. Install NGINX

_sudo apt update_ - update the repo\
_sudo apt upgrade_ - upgrade to latest versions\
_sudo apt install nginx_ - install NGINX\
_curl http://localhost:80_ - test the webserver

![nginx](nginx.JPG)

2. Install MySQL

_sudo apt install mysql-server_ - install mysql\
_sudo mysql\_secure\_installation_ - run native installation security tool\
_sudo mysql_ - test mysql

3. Install PHP

_sudo apt install php-mysql php-fpm_ - install php, php-mysql connector, php-nginx connector

4. Connect NGINX to PHP

_sudo mkdir /var/www/lempproject_ - make a dorectory to hold website\
_sudo chown -R $USER:$USER /var/www/lempproject_ - change ownership of the file\
_sudo nano /etc/nginx/site-avaialable/lempproject_ - make config file and fill as below

```shell
    \#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```
_sudo ln -s /etc/nginx/sites-available/lempproject /etc/nginx/sites-enabled/_ - make symbolic link to the configuration\
_sudo nginx -t_ - test the syntax of the configuration\
_sudo unlink /etc/nginx/sites-enabled/default_ - unlink the default host listening on port 80\
_sudo echo "some data" >> /var/www/lempproject/index.html_ - create test page\
_curl http://localhost:80_ - test the site

5. test the PHP on NGINX

