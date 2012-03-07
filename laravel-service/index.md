---
layout: default
title: Service Bundle
fork-path: https://github.com/sparksp/laravel-service
---

<header class="jumbotron subhead" id="overview">
	<h1>Service Bundle</h1>
    <p class="lead">Simplified service routing for <a href="http://laravel.com">Laravel</a>.</p>
</header>

##Install with Artisan

	php artisan bundle:install service

##Bundle Registration

{% highlight php startinline %}
'service' => array(
	'auto' => true, // Load some default services
	'autoloads' => array(
		'map' => array(
			'Service' => '(:bundle)/service.php',
		),
	),
),
{% endhighlight %}

##Method A (Recommended)

The Service class extends the Laravel\Response class and provides some extended Route methods too.  The methods all follow the same pattern.

{% highlight php startinline %}
Service::get    (string $route, string[] $allowed, Closure|array $action)
Service::put    (string $route, string[] $allowed, Closure|array $action)
Service::post   (string $route, string[] $allowed, Closure|array $action)
Service::delete (string $route, string[] $allowed, Closure|array $action)
Service::any    (string $route, string[] $allowed, Closure|array $action)
{% endhighlight %}

<table class="table table-condensed">
	<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
	<tr><td>$route</td><td>string</td>
		<td><p>A normal route.</p>
			<p><em>Note: The Service class currently supports only a string here.</em></p>
	</td></tr>
	<tr><td>$allowed</td><td>string[]</td>
		<td><p>An array of the service types you wish to allow for this route.</p>
			<p>The type is auto-detected based on this list, if the request is for an unspecified type, or the type is not a registered service then a 404 error response will be returned.</p>
			<p>The first type in the $allowed list is the default type, used for the raw route.  If you do not want a default pass null as the first type.</p>
	</td></tr>
	<tr><td>$action</td><td>Closure|array</td>
		<td><p>Just like a route action except that the first parameter to the Closure will be a Service, any route parameters will be passed in after the service.</p>
			<p>Any response returned from the Closure will be returned by the route, if you do not return anything then the service handler will kick in and generate an appropriate response.  This is useful for handling HTML where you will want to configure the view yourself.</p>
		</td></tr>
</table>

###Example

{% highlight php startinline %}
Service::get('user/(:any)', array('html', 'json', 'xml'), function(Service $service, $slug)
{
	$service->data['user'] = User::where_slug($slug);
	
	// Handle HTML type
	if ($service->type == 'html')
	{
		return View::make('user.show', array(
			'user' => $service->data['user']
		));
	}
});
{% endhighlight %}

##Method B (Alternative)

The Service class also provides a way of using Services within existing routes.

{% highlight php startinline %}
Service::respond (string|null $type, string[] $allowed, Closure $callback, array $args = array())
{% endhighlight %}

<table class="table table-condensed">
	<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
	<tr><td>$type</td><td>string|null</td>
		<td><p>An override type, you can use this to force a type (useful for using file extensions).</p>
			<p>If you pass null here then the Service detector will kick in and guess the route based on the allowed list.</p>
			<p><em>Note: You cannot force a $type that is not in the $allowed list.</em></p>
		</td></tr>
	<tr><td>$allowed</td><td>string[]</td>
		<td><p>The same as Service::get()</p>
		</td></tr>
	<tr><td>$callback</td><td>Closure</td>
		<td><p>A Closure with a single parameter, the Service.</p>
			<p>If you want to pass data into your closure then "use" and $args are your friends.</p>
			<p>Everything else about the Closure is the same as Method A.</p>
		</td></tr>
	<tr><td>$args</td><td>array</td>
		<td><p>An optional array of parameters to be passed to $callback after the Service.</p>
		</td></tr>
</table>

###Example

{% highlight php startinline %}
Route::get(array('user/(:any)', 'user/(:any).(json|xml)'), function($slug, $type = null)
{
	return Service::respond($type, array('html', 'json', 'xml'), function(Service $service) use ($slug)
	{
		$service->data['user'] = User::where_slug($slug);

		// Handle HTML type
		if ($service->type == 'html')
		{
			return View::make('user.show', array(
				'user' => $service->data['user']
			));
		}
	});
});
{% endhighlight %}
