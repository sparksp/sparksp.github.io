---
layout: default
title: ApiGen
fork-path: https://github.com/sparksp/laravel-apigen
---

# ApiGen Bundle

A Laravel bundle for generating PHP Documentation for your code using [ApiGen](http://apigen.org/).

## Installation

<p><strong class="label label-info">Tip</strong> You must have 'apigen' installed and in your path for this bundle to work.</p>

Install via the Artisan CLI:

    php artisan bundle:install apigen

Or download the zip and unpack into your bundles directory.

## Bundle Registration

Just add `'apigen'` to your **application/bundles.php** file.

## Generate

Generate API Documentation for the application:

	php artisan apigen::make

Generate API Documentation for Laravel:

	php artisan apigen::make:core

Generate API Documentation for a bundle:

	php artisan apigen::make:bundle {name}

Generate API Documentation for all bundles:

	php artisan apigen::make:bundle

Generate API Documentation for everything:

	php artisan apigen::make:all

##Configure

You can add **apigen.neon** files to any of the above directories and they will get mixed in with our defaults.  However, the destination will always be **api**.

You can also configure the default apigen options in **config/default.php**.