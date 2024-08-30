# Steps to Migrate an Laravel App 5.6 to 11

## Update to Laravel 5.8:
- Initially you have rh 9.4 and php 7.4.
- Use root as user
- Set apache como owner de carpeta storage
  chown -Rfv apache:apache .
  chmod -R 775 storage bootstrap/cache
### Composer
- rm console.lock
- composer self-update
- set consoletds/charts: “6.*”, in composer.json
- composer update consoletvs/charts
-./vendor/bin/upgrade-carbon (Y)
- It was updated to version 5.8 (it was found vulnerabilities)

## Installation of PHP 8.2
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
  
 
