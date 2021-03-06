A content management system for [Laravel 5](http://laravel.com/).

http://cmscanvas.com/

[![Latest Stable Version](https://poser.pugx.org/diyphpdeveloper/cmscanvas/v/stable)](https://packagist.org/packages/diyphpdeveloper/cmscanvas)
[![Total Downloads](https://poser.pugx.org/diyphpdeveloper/cmscanvas/downloads)](https://packagist.org/packages/diyphpdeveloper/cmscanvas)
[![Latest Unstable Version](https://poser.pugx.org/diyphpdeveloper/cmscanvas/v/unstable)](https://packagist.org/packages/diyphpdeveloper/cmscanvas)
[![License](https://poser.pugx.org/diyphpdeveloper/cmscanvas/license)](https://packagist.org/packages/diyphpdeveloper/cmscanvas)

# Requirements

CMS Canvas requires Laravel 5.2 and a MySQL server.

# Installation

Require this package with Composer

```bash
composer require diyphpdeveloper/cmscanvas:2.0.*
```

Create the database

```bash
mysql -uroot -p -e "create database cmscanvas"
```

Update your .env file or config/database.php to use the cmscanvas database

```bash
...
DB_HOST=localhost
DB_DATABASE=cmscanvas
DB_USERNAME=root
DB_PASSWORD=root
...
```

# Quick Start

Once Composer has installed or updated you will need to register CMS Canvas with Laravel itself. Open up config/app.php and find the providers key, towards the end of the file, and add the following just prior to the application service providers:

```php
'providers' => [
    ...
        CmsCanvas\Providers\CmsCanvasServiceProvider::class,
        CmsCanvas\Providers\RouteServiceProvider::class,
        CmsCanvas\Providers\EventServiceProvider::class,
        Collective\Html\HtmlServiceProvider::class,
        Intervention\Image\ImageServiceProvider::class,
        TwigBridge\ServiceProvider::class,

        /*
         * Application Service Providers...
         */
    ...
],
```

Now find the alliases key, again towards the end of the file, and add the following to the end:

```php
'aliases' => [
    ...
        'Admin'     => CmsCanvas\Support\Facades\Admin::class,
        'Content'   => CmsCanvas\Support\Facades\Content::class,
        'Theme'     => CmsCanvas\Support\Facades\Theme::class,
        'Form'      => Collective\Html\FormFacade::class,
        'HTML'      => Collective\Html\HtmlFacade::class,
        'Twig'      => TwigBridge\Facade\Twig::class,
        'StringView' => TwigBridge\Facade\StringView::class,
],
```

Update the providers array in config/auth.php to use CMS Canvas's user model:

```php
'providers' => [
    'users' => [
        'driver' => 'eloquent',
        'model' => CmsCanvas\Models\User::class,
    ],
],
```

Now that config/app.php and config/auth.php is configured, use Artisan to add CMS Canvas's templates and configs:

```php
php artisan vendor:publish
```

Next use Artisan to create CMS Canvas's database tables:

```php
php artisan migrate
```

Populate the database tables with the default data required for CMS Canvas to run:

```php
php artisan db:seed --class="CmsCanvas\Database\Seeds\DatabaseSeeder"
```

Make the following directories writable:

```bash
chmod 777 public/diyphpdeveloper/cmscanvas/thumbnails
chmod 777 public/diyphpdeveloper/cmscanvas/uploads
```

Finally, remove any root (home page) routes from app/Http/routes.php

```php
// app/Http/routes.php
// The following is an example of what to remove:
- Route::get('/', function () {
-     return view('welcome');
- });
```

To access the admin panel go to your web browser and visit:

```
http://yourdomain.com/sitemin
Email: admin@domain.com
Password: password

```

Once you are logged in the first thing you should do is change your email and password!!!
