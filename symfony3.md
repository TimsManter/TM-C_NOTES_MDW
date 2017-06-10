# Symfony3

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreateDate: 2017-01
* @BasedOn: [Documentation][basedon]

[basedon]: https://symfony.com/

<!-- TOC -->

- [Intstallation](#intstallation)
  - [Symfony Installer](#symfony-installer)
  - [Composer](#composer)
- [Setup](#setup)
  - [Internal server](#internal-server)
  - [Check configuration](#check-configuration)
  - [Install dependencies](#install-dependencies)
  - [Update dependencies](#update-dependencies)
- [Controller](#controller)
- [Router](#router)
  - [Requirements](#requirements)
  - [Redirect](#redirect)
  - [JSON](#json)
- [Doctrine](#doctrine)
  - [Types of data](#types-of-data)

<!-- /TOC -->

## Intstallation

### Symfony Installer
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

## Controller

```php
// src/AppBundle/Controller/LuckyController.php
namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

class LuckyController extends Controller
{
  /**
    * @Route("/lucky/number")
    */
  public function numberAction(Request $request)
  {
    $number = mt_rand(0, 100);

    return new Response(
      '<html><body>Lucky number: '.$number.'</body></html>'
    );
  }
}
```

## Router

> Note: Annotations values have to be in " quotes instead of ' ones.

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

### Redirect

```php
// redirect to the "homepage" route
return $this->redirectToRoute('homepage');

// do a permanent - 301 redirect
return $this->redirectToRoute('homepage', array(), 301);

// redirect to a route with parameters
return $this->redirectToRoute('blog_show', array('slug' => 'my-page'));

// redirect externally
return $this->redirect('http://symfony.com/doc');
```

### JSON

```php
// returns '{"username":"jane.doe"}' and sets the proper Content-Type header
return $this->json(array('username' => 'jane.doe'));

// the shortcut defines three optional arguments
// return $this->json($data, $status = 200, $headers = array(), $context = array());
```

## Doctrine

### Types of data

Type | Size | PHP type | Description
-----|------|----------|------------
smallint|2B|integer|0 to 65535 or −32768 to 32767
integer|4B|integer|0 to 4294967295 or −2147483648 to 2147483647
bigint|8B|string|
decimal||string|
float||float/double|
string||string|Limited length
text||string|Unlimited length
guid||string|"Globally Unique Identifier"
binary||resource|Limited length
blob||resource|Unlimited length
boolean|1b|boolean|true or false
date|date only|\DateTime|
date_immutable|date only|\DateTimeImmutable|
datetime|date & time|\DateTime
datetime_immutable|date & time|\DateTimeImmutable|
datetimetz|date, time, timezone|\DateTime|
datetimetz_immutable|date, time, timezone|\DateTimeImmutable|
time|time only|\DateTime|
time_immutable|time only|\DateTimeImmutable|
dateinterval|date & time difference|\DateInterval|
array||array|serialization
simple_array||array[string]|implode()/explode() with comma delimeter
json||array|json_decode()
json_array||array|**deprecated**
object||object|serialization