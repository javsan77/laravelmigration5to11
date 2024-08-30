### Steps to Migrate an Laravel App 5.6 to 11

## Update to Laravel 5.8:

- Installation of Red Hat 9.4
- Use root as user
- Installation of Nginx

# Installation of PHP 8.2
  dnf module disable php
  dnf remove php\*
  sudo systemctl restart nginx
  dnf module disable php
  dnf module enable php:8.2
  dnf update php
  dnf install @php:8.2
  php -v
  dnf install php php-cli php-fpm php-mysqlnd php-opcache php-xml php-gd php-mbstring php-json php-common
  
# Install Git
  yum install git
  
 
