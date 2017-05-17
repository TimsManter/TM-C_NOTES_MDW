# Symfony3

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-01
* @BasedOn: [Documentation][basedon]

[basedon]: https://symfony.com/

<!-- TOC -->

1. [Overview](#overview)
2. [Intstallation](#intstallation)
  1. [Installer](#installer)
  2. [Composer](#composer)
3. [Setup](#setup)
  1. [Internal server](#internal-server)
  2. [Check configuration](#check-configuration)
  3. [Install dependencies](#install-dependencies)
  4. [Update dependencies](#update-dependencies)
4. [Controler](#controler)
5. [Router](#router)
  1. [Requirements](#requirements)

<!-- /TOC -->

## Intstallation

### Installer
`symfony new project_name [2.8]`

### Composer
`composer create-project symfony/framework-standard-edition project_name ["2.8.*"]`

> Note: The last parameter is optional and allows to use specific version

## Setup

### Internal server

`php ./bin/console server:run`

### Check configuration
`http://localhost:8000/config.php`

### Install dependencies
`composer install`

### Update dependencies
`composer update`

## Controler

```php
// src/AppBundle/Controller/LuckyController.php
namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

class LuckyController
{
    /**
     * @Route("/lucky/number")
     */
    public function numberAction()
    {
        $number = mt_rand(0, 100);

        return new Response(
            '<html><body>Lucky number: '.$number.'</body></html>'
        );
    }
}
```

## Router

> Note: Annotations have to be in " quotes instead of ' ones.

```php
/**
    * Matches /blog exactly
    *
    * @Route("/blog", name="blog_list")
    */
public function listAction() { }

/**
    * Matches /blog/*
    *
    * @Route("/blog/{slug}", name="blog_show")
    */
public function showAction($slug) { } // additional parameter
```

### Requirements
`@Route("/blog/{page}", name="blog_list", requirements={"page": "\d+"})`

`@Method({"GET","HEAD"})` only GET or HEAD type of request
`@Method("PUT")` only PUT type of request