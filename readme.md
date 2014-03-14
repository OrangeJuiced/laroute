# Laroute

[Laravel](http://laravel.com/) has some pretty sweet [helper functions](http://laravel.com/docs/helpers#urls) for generating urls/links, it's auto-json-magic makes it building APIs super easy. It's my go-to choice for building single-page js apps.

Wouldn't it be amazing if we could access our Laravel routes from JavasScript?

This package allows us to port our routes over to JavaScript, and gives us a bunch of _very familiar_ helper functions to use.

## Installation

Install the usual [composer](https://getcomposer.org/) way.

###### package.json
```json
{
	"require" : {
		"lord/laroute" : "1.*"
	}
}
```

###### app/config/app.php
```php
	...
	
	'providers' => array(
		...
		'Lord\Laroute\LarouteServiceProvider',
	],
	
	...
```

### Configure (optional)

Copy the packages config files.

```
php artisan config:publish lord/laroute
```

###### app/config/packages/lord/laroute/config.php

```php
<?php

return array(

    'template' => 'vendor/lord/laroute/src/Lord/Laroute/templates/laroute.min.js',

    'path'     => 'public/js',

    'filename' => 'laroute',

    'namespace' => 'laroute',

);

```

### Generate the `laroute.js`

To access the routes, we need to "port" them over to a JavaScript file:

```
php artisan generate:laroute
```

With the default configuration, this will create a `public/js/laroute.min.js` file to include in your page, or build.


## JavaScript Documentation

By default, all of the functions are under the `laroute` namespace. This documentation will stick with this convention.


### action

Generate a URL for a given controller action. 

```js
/** 
 * laroute.action(action, [parameters = {}])
 *
 * action     : The action to route to.
 * parameters : Optional. key:value object literal of route parameters.
 */

laroute.action('HomeController@getIndex');
```

### route

Generate a URL for a given named route.

```js
/**
 * laroute.route(name, [parameters = {}])
 *
 * name       : The name of the route to route to.
 * parameters : Optional. key:value object literal of route parameters.
 */
 
 laroute.route('Hello.{planet}', { planet : 'world' });
```

### link_to

Generate a html link to the given url.

```js
/**
 * laroute.link_to(url, [title = url, attributes = {}]])
 *
 * url        : A relative url.
 * title      : Optional. The anchor text to display
 * attributes : Optional. key:value object literal of additional html attributes.
 */
 
 laroute.link_to('foo/bar', 'Foo Bar', { style : "color:#bada55;" });
```

### link_to_route

Generate a html link to the given route.

```js
/**
 * laroute.link_to_route(name, [title = url, parameters = {}], attributes = {}]]])
 *
 * name       : The name of the route to route to.
 * title      : Optional. The anchor text to display
 * parameters : Optional. key:value object literal of route parameters.
 * attributes : Optional. key:value object literal of additional html attributes.
 */
 
 laroute.link_to_route('home', 'Home');
```

### link_to_action

Generate a html link to the given action.

```js
/**
 * laroute.link_to_action(action, [title = url, parameters = {}], attributes = {}]]])
 *
 * action     : The action to route to.
 * title      : Optional. The anchor text to display
 * parameters : Optional. key:value object literal of route parameters.
 * attributes : Optional. key:value object literal of additional html attributes.
 */
 
 laroute.link_to_action('HelloController@planet', undefined, { planet : 'world' });
```


## Licence

[View the licence in this repo.](https://github.com/aaronlord/laroute/blob/master/LICENSE)
