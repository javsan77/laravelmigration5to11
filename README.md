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
  ```json
  "require":{
     "php":"^7.2",
     "fideloper/proxy":"^4.2",
     "laravel/framework":"^6.0",
     "laravel/tinker":"^1.0"
   }
  ```
-  composer update
## Update to Laravel 7:
- In composer.json, add "laravel/ui": "^2.4" and modify "laravel/framework": "^7.0. This way:
```json
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
```
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
```
- composer remove illuminate/support laravel/tinker nunomaduro/collision
- composer install
## Update to Laravel 8:
- rm composer.lock
- rm -rf vendor
- in composer.json:
```json
"require": {
    "laravel/ui": "^3.0"
}
```
- composer update
- composer install
## Installation of PHP 8.2
### Method A (RH free)
- dnf install epel-release
- dnf install https://rpms.remirepo.net/enterprise/remi-release-9.rpm
- dnf module reset php
- dnf module enable php:remi-8.2
- dnf install php php-cli php-fpm php-mysqlnd php-opcache php-xml php-gd php-mbstring php-pdo php-json php-zip php-curl
- systemctl restart httpd

### Method B (RH licensed)
  - dnf module disable php
  - dnf remove php\*
  - systemctl restart nginx
  - dnf module disable php
  - dnf module enable php:8.2
  - dnf update php
  - dnf install @php:8.2
  - php -v
  - dnf install php php-cli php-fpm php-mysqlnd php-opcache php-xml php-gd php-mbstring php-json php-common
  - yum install git

- in composer.json
```json
"require": {
    "php": "^8.0",
    "fideloper/proxy": "^4.4.1",
    "fruitcake/laravel-cors": "^2.0",
    "guzzlehttp/guzzle": "^7.0.1",
    "laravel/framework": "^9.0",
    "laravel/tinker": "^2.6"
}
```
```json
    "require-dev": {
        "filp/whoops": "^2.0",
        "fzaninotto/faker": "^1.4",
        "mockery/mockery": "^1.0",
        "phpunit/phpunit": "^9.5"
    },
```
- rm composer.lock
- rm -rf vendor
- composer update
- composer install
## PSR-4 autoloading standard (Optional):
- Inside app/Helpers, Add in the begin of File Pdf.php :
```php
<?php
namespace App\Helpers;
use Fpdf\Fpdf;
```
- Funciones.php:
```php
<?php
namespace App\Helpers;
```
-  in composer.json
```json
"autoload": {
        "classmap": [
            "database/seeds",
            "database/factories",
            "app/Helpers/fpdf181"
        ],
	"files": [
            "app/Helpers/Funciones.php",
            "app/Helpers/Pdf.php"
        ],
	"psr-4": {
            "App\\": "app/"
        }
```
- composer require fpdf/fpdf
- composer install
## Update to Laravel 9:
- rm -rfv composer.lock vendor
- in composer.json:
```json
"require": {
    "php": "^8.0",
    "laravel/framework": "^9.0",
    // other dependencies...
}
```
- composer self-update
- composer remove barryvdh/laravel-cors
- composer require fruitcake/laravel-cors
- Update your app/Http/Kernel.php to use the new CORS middleware if needed:
```php
<?php
 ...
protected $middleware = [
    \Fruitcake\Cors\HandleCors::class,
    // other middleware
];
```
- php artisan vendor:publish --tag="cors"
- composer update
- composer install
## Update to Laravel 10:
- rm -rfv composer.lock vendor
- in composer.json remove "fruitcake/laravel-cors" from your composer.json (require section) and:
```json
"require": {
    "php": "^8.1",
    ...
    "laravel/framework": "^10.0",
    "laravel/ui": "^4.0",
    ...
}
```
- in app/Http/Kernel.php Replace \Fruitcake\Cors\HandleCors::class, with \Illuminate\Http\Middleware\HandleCors::class, 
- composer self-update
- composer remove fideloper/proxy
- composer update
- composer install (por demás)
## Update to Laravel 11:
- rm -rfv composer.lock vendor
- in composer.json:
```json
"require": {
    "laravel/framework": "^11.0",
     ….
    "nunomaduro/collision": "^8.0"
}
```
```json
    "require-dev": {
       ….
        "phpunit/phpunit": "^11.0"
    },
```
- composer update
- composer remove fzaninotto/faker
- composer require fakerphp/faker --dev
- composer self-update
- composer install

## Set online app:
- Create .htaccess on root directory with this content (for public folder is set correctly and jquery load ok):
  ```json
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews -Indexes
    </IfModule>

    RewriteEngine On

    # Handle Authorization MemberHeader
    RewriteCond %{HTTP:Authorization} .
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

    # Redirect Trailing Slashes If Not A Folder...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_URI} (.+)/$
    RewriteRule ^ %1 [L,R=301]

    # Remove public URL from the path
    RewriteCond %{REQUEST_URI} !^/public/
    RewriteRule ^(.*)$ /public/$1 [L,QSA]

    # Handle Front Controller...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]
</IfModule>
```
- su
- sudo chown -Rfv apache:apache .
- getenforce -> Permissive
- Update Your App\Http\Middleware\TrustProxies
```php
namespace App\Http\Middleware;

use Illuminate\Http\Middleware\TrustProxies as Middleware;

class TrustProxies extends Middleware
{
    // You can configure the trusted proxies and headers here
}
```
- Check Kernel.php: Ensure that your app/Http/Kernel.php does not reference the old TrustProxies class. It should look like this:
```php
protected $middleware = [
    \App\Http\Middleware\TrustProxies::class,
    // Other middleware...
];
```
- /var/www/html/app/Http/Middleware/TrustProxies.php
- Modify TrustProxies.php to Remove the headers Property:
You don't need to explicitly set the $headers property. Laravel's TrustProxies middleware handles proxy headers internally with sensible defaults.
```php
<?php

namespace App\Http\Middleware;

//use Illuminate\Http\Request;
//use Fideloper\Proxy\TrustProxies as Middleware;
use Illuminate\Http\Middleware\TrustProxies as Middleware;
//use Illuminate\Http\Request;
//use Fideloper\Proxy\TrustProxies as BaseTrustProxies;
//use Symfony\Component\HttpFoundation\Request as SymfonyRequest;

class TrustProxies extends Middleware
{
    /**
     * The trusted proxies for this application.
     *
     * @var array
     */
    protected $proxies;

    /**
     * The headers that should be used to detect proxies.
     *
     * @var int
     */
    //protected $headers = Request::HEADER_X_FORWARDED_ALL;
    //protected $headers = SymfonyRequest::HEADER_X_FORWARDED_ALL;
}
```
- php artisan config:clear
- php artisan cache:clear
- php artisan route:clear
 -php artisan view:clear
- If it appears error con this last command, then Update the config/cache.php (91) and config/session.php (127) Files: Replace the str_slug function call with Str::slug. Ensure you import the Str facade at the top of the file.
- rm composer.lock
- rm -rf vendor
- composer remove barryvdh/laravel-cors . If failed , then :
- composer clear-cache
- composer update laravel/framework


