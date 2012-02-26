---
layout: default
title: Gravitas
fork-path: https://github.com/sparksp/laravel-gravatar
---

# Gravitas Bundle

Basic [Gravatar](http://gravatar.com/) support for Laravel.

## Installation

Install via the Artisan CLI:

	php artisan bundle:install gravitas

Or download the zip and unpack into your bundles directory.

## Bundle Registration

Add the following to your **application/bundles.php** file:

{% highlight php startinline %}
'gravitas' => array(
	'autoloads' => array(
		'map' => array(
			'Gravitas\\API' => '(:bundle)/api.php',
		),
	),
),
{% endhighlight %}

## Guide

Get a Gravatar URL

{% highlight php startinline %}
Gravitas\API::url('me@phills.me.uk', 120);
{% endhighlight %}

Get the HTML for a Gravatar image

{% highlight php startinline %}
Gravitas\API::image('me@phills.me.uk', null, 'Phill Sparks');
{% endhighlight %}

## Configure

You can configure the size, rating and default image in **config/default.php**.  Full documentation is included in the config file.