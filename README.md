# Laravel Mentions

[![Build Status](https://img.shields.io/travis/faustbrian/Laravel-Mentions/master.svg?style=flat-square)](https://travis-ci.org/faustbrian/Laravel-Mentions)
[![PHP from Packagist](https://img.shields.io/packagist/php-v/faustbrian/laravel-mentions.svg?style=flat-square)]()
[![Latest Version](https://img.shields.io/github/release/faustbrian/Laravel-Mentions.svg?style=flat-square)](https://github.com/faustbrian/Laravel-Mentions/releases)
[![License](https://img.shields.io/packagist/l/faustbrian/Laravel-Mentions.svg?style=flat-square)](https://packagist.org/packages/faustbrian/Laravel-Mentions)

This package makes it possible to create text/textarea fields that enable **mentioning** by using [At.js](https://github.com/ichord/At.js).

The data for the autocomplete is loaded from a route which will load data based on predefined key-value pairs of an alias and a model in the config.

## Installation

Require this package, with [Composer](https://getcomposer.org/), in the root directory of your project.

``` bash
$ composer require faustbrian/laravel-mentions
```

If you need to modify the configuration or the views, you can run:

```bash
php artisan vendor:publish --provider="BrianFaust\Mentions\MentionsServiceProvider"
```

The package views will now be located in the `app/resources/views/vendor/mentions/` directory and the configuration will be located at `app/config/mentions.php`.

## Configuration

To make it possible for At.js to load data we need to define key-value pairs that consist of an alias and a corresponding model.

``` php
return [

    'users'    => 'App\User',      // responds to /api/mentions/users
    'friends'  => 'App\Friend',    // responds to /api/mentions/friends
    'clients'  => 'App\Client',    // responds to /api/mentions/clients
    'supports' => 'App\Supporter', // responds to /api/mentions/supports

];
```

So now with these `aliases` configured we could create a new textfield which will send a request to the `users` route and search for matching data in the `name` column.

``` php
{!! mention()->asText('recipient', old('recipient'), 'users', 'name') !!}
```

## Usage

```html
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Laravel PHP Framework</title>
        <link rel="stylesheet" type="text/css" href="/styles/jquery.atwho.min.css">
    </head>

    <body>
        <div class="container">
            {!! mention()->asText('recipient', old('recipient'), 'users', 'name') !!}
            {!! mention()->asTextArea('message', old('message'), 'users', 'name') !!}
        </div><!-- /.container -->

        <!-- Requirements -->
        <script src="//code.jquery.com/jquery-2.1.3.min.js"></script>
        <script src="/scripts/jquery.atwho.min.js"></script>
        <script src="/scripts/jquery.caret.min.js"></script>
        <!-- Laravel Mentions -->
        @include('mentions::assets')
    </body>
</html>
```

## Testing

``` bash
$ phpunit
```

## Security

If you discover a security vulnerability within this package, please send an e-mail to hello@brianfaust.me. All security vulnerabilities will be promptly addressed.

## Credits

- [Brian Faust](https://github.com/faustbrian)
- [All Contributors](../../contributors)

## License

[MIT](LICENSE) © [Brian Faust](https://brianfaust.me)
