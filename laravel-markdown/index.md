---
layout: default
title: Sparkdown Bundle
fork-path: https://github.com/sparksp/laravel-markdown
---

# Sparkdown Bundle

A simple bundle to provide [Markdown](http://daringfireball.net/projects/markdown/) and [Markdown Extra](http://michelf.com/projects/php-markdown/) functions.

Links and image URLs are passed through Laravel\URL::to and Larave\URL::to_asset.

## Installation

Install via the Artisan CLI:

{% highlight bash %}
php artisan bundle:install sparkdown
{% endhighlight %}


Or download the zip and unpack into your bundles directory.

## Bundle Registration

Just add `'sparkdown'` to your **application/bundles.php** file.

## Guide

### Parse some text

Start the bundle and use Sparkdown\Markdown

{% highlight php startinline %}
Bundle::start('sparkdown');
echo Sparkdown\Markdown($text);
{% endhighlight %}

### View a markdown file

You can create Sparkdown\View objects, like Laravel\View objects

{% highlight php startinline %}
Router::register('GET /about', function()
{
	// View of application/views/about.md
	return Sparkdown\View::make('about');

	// Also supports bundles and paths...
	// View of bundles/bundle/views/path/file.md
	return Sparkdown\View::make('bundle::path.file');
});
{% endhighlight %}

And you can route to the handy controller (needs 1 parameter).

{% highlight php startinline %}
Route::get('(about)', 'sparkdown::page@show');
{% endhighlight %}
