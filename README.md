Dwoo
====

Dwoo is a PHP5/PHP7 Template Engine that was started in early 2008. The idea came
from the fact that Smarty, a well known template engine, is getting older and
older. It carries the weight of it's age, having old features that are
inconsistent compared to newer ones, being written for PHP4 its Object
Oriented aspect doesn't take advantage of PHP5's more advanced features in
the area, etc. Hence Dwoo was born, hoping to provide a more up to date and
stronger engine.

So far it has proven to be faster than Smarty in many areas, and it provides
a compatibility layer to allow developers that have been using Smarty for
years to switch their application over to Dwoo progressively.

> Dwoo **1.3.x** is compatible from **PHP 5.3.x** to **PHP 7.x**

About this fork
===============

We have been using Dwoo in BlackCat CMS for a very long time and are still very satisfied with its performance and easy extensibility. For this reason and because changing all the templates would be a considerable effort, we created this fork to make Dwoo run with PHP8. Although we created this fork primarily for BlackCat CMS, there is nothing to be said against using it outside of it. Although we don't plan to add more features, reprogram everything or officially support Dwoo, we're happy to look at pull requests or issues.

> This fork is tested with **PHP 8.0 RC4** at the moment.

Requirements
------------
* PHP >= **7.2**
* PHP >= **8.0 RC4**
* [Multibyte String](http://php.net/manual/en/book.mbstring.php)

License
=======
Dwoo is released under the [GNU LESSER GENERAL PUBLIC LICENSE V3](./LICENSE.md) license.

Quick start - Running Dwoo
==========================

Basic Example
-------------
```php
<?php
// Include Composer autoloader
require __DIR__ . '/vendor/autoload.php';

// Create the controller, this is reusable
$dwoo = new Dwoo\Core();

// Load a template file (name it as you please), this is reusable
// if you want to render multiple times the same template with different data
$tpl = new Dwoo\Template\File('path/to/index.tpl');

// Create a data set, if you don't like this you can directly input an
// associative array in $dwoo->get()
$data = new Dwoo\Data();
// Fill it with some data
$data->assign('foo', 'BAR');
$data->assign('bar', 'BAZ');

// Outputs the result ...
echo $dwoo->get($tpl, $data);
// ... or get it to use it somewhere else
$dwoo->get($tpl, $data);
```

Loop Example
------------
```php
<?php
// To loop over multiple articles of a blog for instance, if you have a
// template file representing an article, you could do the following :

require __DIR__ . '/vendor/autoload.php';

$dwoo = new Dwoo\Core();
$tpl = new Dwoo\Template\File('path/to/article.tpl');

$pageContent = '';
$articles = array();

// Loop over articles that have been retrieved from the DB
foreach($articles as $article) {
    // Either associate variables one by one
    $data = new Dwoo\Data();
    $data->assign('title', $article['title']);
    $data->assign('content', $article['content']);
    $pageContent .= $dwoo->get($tpl, $data);

    // Or use the article directly (which is a lot easier in this case)
    $pageContent .= $dwoo->get($tpl, $article);
}
```
