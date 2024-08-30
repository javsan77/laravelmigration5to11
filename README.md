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
## Update to Laravel 6:
- nano composer.json
  "require":{
     "php":"^7.2",
     "fideloper/proxy":"^4.2",
     "laravel/framework":"^6.0",
     "laravel/tinker":"^1.0"
   }
-  composer update
## Update to Laravel 7:
- In composer.json, add "laravel/ui": "^2.4" and modify "laravel/framework": "^7.0. This way:

    "require": {
        "php": "^7.1.3",
        "barryvdh/laravel-cors": "^1.0",
        "consoletvs/charts": "6.*",
        "econea/nusoap": "~0.9.5.1",
        "fideloper/proxy": "^4.0",
        "laravel/framework": "^7.0",
        "laravel/ui": "^2.4",
        "muhamadrezaar/highcharts": "dev-master"
    },

- nano /var/www/html/app/Exceptions/Handler.php

Change a:
```php
<?php

namespace App\Exceptions;

use Throwable;
use Illuminate\Foundation\Exceptions\Handler as ExceptionHandler;

class Handler extends ExceptionHandler
{
    /**
     * A list of the exception types that are not reported.
     *
     * @var array
     */
    protected $dontReport = [
        //
    ];

    /**
     * A list of the inputs that are never flashed for validation exceptions.
     *
     * @var array
     */
    protected $dontFlash = [
        'password',
        'password_confirmation',
    ];

    /**
     * Report or log an exception.
     *
     * @param  \Throwable $exception
     * @return void
     */
    public function report(Throwable $exception)
    {
     	parent::report($exception);
    }

    /**
     * Render an exception into an HTTP response.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Throwable  $exception
     * @return \Illuminate\Http\Response
     */
    public function render($request, Throwable $exception)
    {
     	return parent::render($request, $exception);
    }
}

`?>`

- composer remove illuminate/support laravel/tinker nunomaduro/collision
- composer install

*******************************




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
  
 
