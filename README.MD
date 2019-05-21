CurlerBundle
====================================

This bundle wraps [Curler](https://github.com/wernerdweight/Curler) into Symfony Bundle.

[![Build Status](https://travis-ci.org/wernerdweight/CurlerBundle.svg?branch=master)](https://travis-ci.org/wernerdweight/CurlerBundle)
[![Latest Stable Version](https://poser.pugx.org/wernerdweight/curler-bundle/v/stable)](https://packagist.org/packages/wernerdweight/curler-bundle)
[![Total Downloads](https://poser.pugx.org/wernerdweight/curler-bundle/downloads)](https://packagist.org/packages/wernerdweight/curler-bundle)
[![License](https://poser.pugx.org/wernerdweight/curler-bundle/license)](https://packagist.org/packages/wernerdweight/curler-bundle)


Installation
------------

1) Download using composer

```bash
composer require wernerdweight/curler-bundle
```

2) Enable the bundle

Enable the bundle in your kernel:

```php
    <?php
    // config/bundles.php
    return [
        // ...
        WernerDweight\CurlerBundle\CurlerBundle::class => ['all' => true],
    ];
```

3) Use in your project

```php
use WernerDweight\Curler\Curler;
use WernerDweight\Curler\Request;

class MyService
{
    /** Curler */
    private $curler;
     
    /**
     * @param Curler $curler
     */
    public function __construct(Curler $curler)
    {
        $this->curler = $curler;
    }
    
    public function myAction(): void
    {
        $request = (new Request())
            ->setEndpoint('https://some-website.tld')
            ->setMethod('POST')
            ->setPayload(['key' => 'value'])
            ->setHeaders(['Accept: text/html', 'Accept-Encoding: gzip'])
            ->setAuthentication('user', 'password')
        ;
        $response = $this->curler->request($request);
        echo $response->text();  // '<html>...</html>'
        var_dump($response->getMetaData()); // array of response metadata (content-type, status...)
    }
}
```

License
-------
This bundle is under the MIT license. See the complete license in the root directiory of the bundle.
