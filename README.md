## quickassets

QuickAssets is a simple script in development with the goal of making it easier to generate cache-bustable URLs in PHP.

The goal is to create a simple framework for defining a server (or multiple servers) and automatically setting cache-friendly URLs. You should be handling the actual caching yourself, either with server-side Apache/Nginx settings or with a cache engine like Varnish (or both).

**NOTE:** If you're a legacy user of QuickAssets, [you'll want to read this](https://github.com/vanpattenmedia/quickassets/wiki/Upgrading-to-QuickAssets-1.0).

### Using QuickAssets

Getting started with QuickAssets is easy. First, add QuickAssets to your composer.json file:

```json
{
	"require": {
		"vanpattenmedia/quickassets": "dev-master"
	}
}
```

Then, install QuickAssets with `composer install`.

In your project's code, after requiring the Composer autoloader, use QuickAssets and instantiate it:

```php
use VanPattenMedia\QuickAssets\QuickAsset;

$a = new QuickAsset();
```

Next, set up an asset type:

```php
$a->addAssetType('css', array(
	'assetPath' => 'assets/stylesheets',
	'rootPath'  => __DIR__ . '../../public/assets/stylesheets',
));
```

Bind your asset type to a new host:

```php
$a->addHost('/', array(
	'assetTypes' => [ 'css' ],
));
```

Echo the result in your template file:

```php
<link rel="stylesheet" href="<?php echo $a->url('css', 'style.css'); ?>">
```

And you'll get:

```php
<link rel="stylesheet" href="/assets/stylesheets/style.css?20130626010446">
```

[Consult the wiki](https://github.com/vanpattenmedia/quickassets/wiki) for more examples and to learn how to change the display of your cache busting string, as well as its contents.

### Twig Extension

Version 1.5 introduces an extension for Twig, the popular PHP template engine. This makes it easier to include your assets in Twig templates.

To get started, instantiate the `QuickAsset` object and add your configuration (abbreviated example):

```php
$quickAsset = new \VanPattenMedia\QuickAssets\QuickAsset();

$quickAsset->addAssetType( 'css', arr...
```

Once you're set up, add the extension and pass in your object:

```php
$twig->addExtension( new \VanPattenMedia\QuickAssets\TwigExtension( $quickAsset ) );
```

You can now access the QuickAssets URL function within Twig:

```twig
This is an image:

<img src="{{ asset_url( 'img', 'pizza.jpg' ) }}">
```

## MIT License
Copyright © Van Patten Media Inc., <http://www.vanpattenmedia.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
