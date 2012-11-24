# Underscore.php [![Build Status](https://secure.travis-ci.org/Anahkiasen/underscore-php.png?branch=master)](https://travis-ci.org/Anahkiasen/underscore-php)
## A redacted port of Underscore.js

Underscore.php is a _redacted_ PHP port of Underscore.js. Its goal is to ease the working and manipulation of arrays, strings and such in PHP development. When I say redacted I mean that all methods were not just imported and converted blatantly — a lot of thought was put into removing methods that were unuseful to PHP developers, changing terms to make them less confusing in a PHP world, and add a lot of new methods and helpers on top of a new elegant syntax.
It can be used both as a static class, and an Object-Oriented class, so both the following are valid :

```php
$array = array(1, 2, 3);

// One-off calls to helpers
Underscore::each($array, function($value) { return $value * 2; })
underscore($array)->each(function($value) { return $value * 2; })

// Or chain calls
underscore($array)->filter(...)->sort(...)->get(2)
Underscore::chain($array)->filter(...)->sort(...)->get(2)
```

You can also alias Underscore's core classes and call them at any time, this mostly provides syntaxic elegance :

```php
// One-off calls
Arrays::first(...)
Arrays::each(...)
String::escape(...)

// Chained calls
Arrays::from($array)->filter(...)->get(2)
```

The core concept is this : static calls return values from their methods, while chained calls update the value of the object they're working on. Which means that an Underscore object don't return its value until you call the `->obtain` method on it — until then you can chain as long as you want, it will remain an object.
The exception are certains properties that are considered _breakers_ and that will return the object's value. An example is `Arrays->get`.

## Customizing Underscore

Underscore.php provides the ability to extend any class with custom functions so go crazy. Don't forget that if you think you have a function anybody could enjoy, do a pull request, let everyone enjoy it !

```php
String::extend('summary', function($string) {
  return String::limit($string, 50, '... — click to read more');
});

String::summary($article->content)
```

It comes with a config file that allows you to alias the main class to whatever you want, the default being `Underscore` and the most common probably being `__` (which is already taken in **Laravel** by the translation helper).
You can also give custom aliases to all of Underscore's methods, in said config file. Just add entries to the `aliases` option, the key being the alias, and the value the method to point to.

## Documentation

You can find a detailed summary of all classes and methods in the [repo's wiki][]

## About underscore.php

There is technically another port of Underscore.js to PHP available [on Github][] — I first discovered it when I saw it was for a time used on Laravel 4. I quickly grew disapoint of what a mess the code was, the lack of updates, and the 1:1 mentality that went behind it.
This revamped Underscore.php doesn't aim to be a direct port of Underscore.js. It sometimes omits methods that aren't relevant to PHP developers, rename others to match terms that are more common to them, provides a richer syntax and leaves room for future methods to be added all the time — whereas the previous port quickly recoded all JS methods to PHP and left it at that.

[repo's wiki]: https://github.com/Anahkiasen/underscore-php/wiki/_pages
[on Github]: https://github.com/brianhaveri/Underscore.php
