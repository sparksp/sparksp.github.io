---
layout: default
title: Τόπος Bundle (Topos)
fork-path: https://github.com/sparksp/laravel-html-menu
---

# Τόπος Bundle (Topos)

A HTML Menu Generator for Laravel.

## Installation

Install via the Artisan CLI:

    php artisan bundle:install topos

Or download the zip and unpack into your **bundles** directory.

## Bundle Registration

You need to register topos with your application before you can use it.  Simply edit **application/bundles.php** and add the following to the array:

{% highlight php startinline %}
'topos' => array(
    'autoloads' => array(
        'map' => array(
            'Topos\\Menu' => '(:bundle)/menu.php',
        ),
    ),
),
{% endhighlight %}

Alternatively you can add just `'topos'` and use `Bundle::start('topos')` each time before you want to make a menu.

## Guide

Generate a simple navigation menu ('ul' is default):

{% highlight php startinline %}
echo Topos\Menu::make(array('class' => 'menu'), 'ol')
    ->add('', 'Home')
    ->add('blog', 'Blog')
    ->add('about', 'About')
    ->add('contact', 'Contact')
    ->render();
{% endhighlight %}

### Optional menu items

You can also use `->add_if($test, $url, $label)` to conditionally add items, test can be any callback or boolean.

{% highlight php startinline %}
echo Topos\Menu::make()
    ->add('', 'Home')
    ->add('blog', 'Blog')
    // Only show the admin item if we're in admin area
    ->add_if(URI::is('admin(/*)?'), 'admin', 'Admin')
    // Only show the logout link if we're logged in
    ->add_if(Auth::check(), 'logout', 'Logout')
    ->render();
{% endhighlight %}
