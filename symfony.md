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
  - [Request](#request)
    - [Available bags](#available-bags)
    - [Methods](#methods)
    - [Headers](#headers)
    - [`ParameterBag` methods](#parameterbag-methods)
  - [Response](#response)
    - [Methods](#methods-1)
    - [Cookies](#cookies)
    - [Redirect](#redirect)
    - [Stream](#stream)
    - [JSON](#json)
- [Router](#router)
  - [Requirements](#requirements)
  - [Redirect](#redirect-1)
  - [JSON](#json-1)
- [Service](#service)
  - [Check services](#check-services)
  - [Aquiring](#aquiring)
  - [Nesting](#nesting)
  - [Parameters](#parameters)
    - [Configuration](#configuration)
    - [Using](#using)
- [Doctrine](#doctrine)
  - [Relations](#relations)
    - [Many to one](#many-to-one)
    - [One to many](#one-to-many)
    - [Many to Many](#many-to-many)
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

### Request
```php
use Symfony\Component\HttpFoundation\Request;

$request = Request::createFromGlobals();
```

#### Available bags
Object | Bag | Class
--- | --- | ---
request | $_POST | ParameterBag
query | $_GET | ParameterBag
cookies | $_COOKIE | ParameterBag
attributes | TODO: Add section | ParameterBag
files | $_FILES | FileBag
server | $_SERVER | ServerBag
headers | Request headers | HeaderBag

#### Methods
Method | Description
--- | ---
getPathInfo() | Relative path
getSession() | Current session
hasPreviousSession() | Check session

#### Headers
Method | Header
--- | ---
getAcceptableContentTypes() | Accept
getLanguages() | Accept-Language
getCharsets() | Accept-Charset
getEncodings() | Accept-Encoding

#### `ParameterBag` methods
Method | Description
--- | ---
all() | All parameters
keys() | All keys
replace() | Replace parameter
add() | Add parameter
get(key, default) | Get parameter value
set() | Set parameter value
has() | Check key in bag
remove() | Remove parameter

### Response
```php
use Symfony\Component\HttpFoundation\Response;

$response = new Response(
    'Content',
    Response::HTTP_OK,
    array('content-type' => 'text/html')
);
```

```php
// Check if valid with request
$response->prepare($request);

// Send
$response->send();
```

#### Methods

Method | Description
--- | ---
setContent(content) | Set content
headers->set(name, value) | Set header
headers->setCookie(cookie) | Set cookie
headers->clearCookie() | Remove cookie
setStatusCode(Response::HTTP_OK) | Set status code
setCharset("UTF-8") | Set charset
send() | Send response

#### Cookies
```php
use Symfony\Component\HttpFoundation\Cookie;

$response->headers->setCookie(new Cookie('foo', 'bar'));
```

#### Redirect

```php
use Symfony\Component\HttpFoundation\RedirectResponse;

$response = new RedirectResponse('http://example.com/');
```

#### Stream
```php
use Symfony\Component\HttpFoundation\StreamedResponse;

$response = new StreamedResponse();
$response->setCallback(function () {
    var_dump('Hello World');
    flush();
    sleep(2);
    var_dump('Hello World');
    flush();
});
$response->send();
```

#### JSON
```php
use Symfony\Component\HttpFoundation\JsonResponse;

// if you know the data to send when creating the response
$response = new JsonResponse(array('data' => 123));

// if you don't know the data to send when creating the response
$response = new JsonResponse();
// ...
$response->setData(array('data' => 123));

// if the data to send is already encoded in JSON
$response = JsonResponse::fromJsonString('{ "data": 123 }');
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

## Service

### Check services

` php bin/console debug:container`

### Aquiring

```php
use Psr\Log\LoggerInterface;

// by type-hint as action method paramether
public function listAction(LoggerInterface $logger)
{
  // or by id (service must be public)
  $logger = $container->get('logger');
}
```

### Nesting

```php
use Psr\Log\LoggerInterface;

class MessageGenerator
{
  private $logger;
  public function __construct(LoggerInterface $logger)
  { // register service by constructor of another service
    $this->logger = $logger;
  }
```

### Parameters

#### Configuration
```yml
# app/config/services.yml
parameters:
  admin_email: manager@example.com

services:
  # ...
  AppBundle\Updates\SiteUpdateManager:
    arguments:
      $adminEmail: '%admin_email%'
```

#### Using
```php
public function newAction()
{
  // controller must extend Controller class
  $adminEmail = $this->getParameter('admin_email');

  // or full path
  $adminEmail = $this->container->getParameter('admin_email');
}
```

## Doctrine

### Relations

#### Many to one
```php
use Doctrine\ORM\Mapping as ORM;

class Product
{
    /**
     * @ORM\ManyToOne(targetEntity="Category", inversedBy="products")
     * @ORM\JoinColumn(name="category_id", referencedColumnName="id")
     */
    private $category;
}
```

#### One to many
```php
use Doctrine\ORM\Mapping as ORM;
use Doctrine\Common\Collections\ArrayCollection;

class Category
{
    /**
     * @ORM\OneToMany(targetEntity="Product", mappedBy="category")
     */
    private $products;

    public function __construct()
    {
        $this->products = new ArrayCollection();
    }
}
```

#### Many to Many

```php
<?php
/**
 * Owning Side
 *
 * @ManyToMany(targetEntity="Group", inversedBy="features")
 * @JoinTable(name="user_groups",
 *  joinColumns={@JoinColumn(name="user_id", referencedColumnName="id")},
 *  inverseJoinColumns={@JoinColumn(name="group_id",
 *    referencedColumnName="id")}
 * )
 */
private $groups;

/**
 * Inverse Side
 *
 * @ManyToMany(targetEntity="User", mappedBy="groups")
 */
private $features;
```

> Note: Don't forget to execute `./bin/console doctrine:generate:entities AppBundle` command.

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