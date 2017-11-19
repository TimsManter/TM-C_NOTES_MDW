# Symfony 3/4

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreateDate: 2017-01
* @BasedOn: [Documentation][basedon]

[basedon]: https://symfony.com/

<!-- TOC -->

- [Intstallation](#intstallation)
- [Setup](#setup)
  - [Internal server](#internal-server)
  - [Install dependencies](#install-dependencies)
  - [Update dependencies](#update-dependencies)
  - [Install more bundles](#install-more-bundles)
- [File tree](#file-tree)
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
  - [Entity](#entity)
  - [`Column` attributes](#column-attributes)
  - [Relations](#relations)
    - [Many to one](#many-to-one)
    - [One to many](#one-to-many)
    - [Many to Many](#many-to-many)
  - [Types of data](#types-of-data)
- [Validation](#validation)
  - [Defining rules](#defining-rules)
  - [Validator](#validator)
  - [Constraints](#constraints)
    - [Basic](#basic)
    - [String](#string)
    - [Number](#number)
    - [Comparison](#comparison)
    - [Date](#date)
    - [Collection](#collection)
    - [File](#file)
    - [Special](#special)
    - [Other](#other)
  - [Targets](#targets)
    - [Property](#property)
    - [Getter](#getter)
    - [Class](#class)

<!-- /TOC -->

## Intstallation

```sh
# uses flex skeleton
> composer create-project symfony/skeleton
```

## Setup

### Internal server

```sh
# for symfony web-server
composer require server
./bin/console server:run
```

### Install dependencies
`composer install`

### Update dependencies
`composer update`

### Install more bundles
```sh
# samples
composer require server
composer require api
composer require admin
composer require orm
composer require log
composer require mailer
```
## File tree

> None: Every directory (even a top one) is optional.
```
/root
|-- assets/
|-- bin/
|    `-- console
|-- config/
|    |-- packages/
|    |    |-- dev/*.yaml
|    |    |-- prod/*.yaml
|    |    |-- test/*.yaml
|    |    `-- *.yaml
|    |-- routes/
|    |    |-- dev/*.yaml
|    |    |-- prod/*.yaml
|    |    |-- test/*.yaml
|    |    `-- *.yaml
|    |-- bundles.php
|    |-- routes.yaml
|    |-- services.yaml
|-- public/
|    `-- index.php
|-- src/
|    |-- Command/*Command.php
|    |-- Controller/**/*Controller.php
|    |-- DataFixtures/*.php
|    |-- Entity/*.php
|    |-- EventSubscriber/*Subscriber.php
|    |-- Form/
|    |    |-- DataTransformer/*Transformer.php
|    |    |-- Type/*Type.php
|    |    `-- *Type.php
|    |-- Repository/*Repository.php
|    |-- Resources/
|    |-- Security/
|    |-- Twig/*Extension.php
|    |-- Utils/*.php
|    |-- Events.php
|    `-- Kernel.php
|-- templates/**/*.html.twig
|-- tests/**/*Test.php
|-- translations/*.xlf
|-- var/
|    |-- cache/
|    |-- data/
|    |-- log/
|    |-- sessions/
|    |-- tmp/
|    `-- SymfonyRequirements.php
|-- vendor/
|-- .env
|-- composer.json
`-- composer.lock
```

## Controller
```php
// src/App/Controller/LuckyController.php
namespace App\Controller;

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

### Entity

```php
// src/Entity/Product.php
namespace App\Entity;

use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity
 * @ORM\Table(name="product")
 */
class Product
{
    /**
     * @ORM\Column(type="integer")
     * @ORM\Id
     * @ORM\GeneratedValue(strategy="AUTO")
     */
    private $id;

    /**
     * @ORM\Column(type="string", length=100)
     */
    private $name;

    /**
     * @ORM\Column(type="decimal", scale=2)
     */
    private $price;

    /**
     * @ORM\Column(type="text")
     */
    private $description;
}
```

### `Column` attributes

> Note: All attributes are optional.

Name | Default | Description
---|---|---
type | string | Mapping type
name | field name | Name of the column in the database
length | 255 | Length of the string
unique | false | Column is a unique key
nullable | false | Value can be null
precision | 0 | Maximum precision of decimal number
scale | 0 | Number of digits in decimal number
columnDefinition | | Custom create snippet
options | Options for database platform when creating

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

Type | PHP type | Description
-----|------|----------|------------
smallint       | integer       | 0 to 65535 or −32768 to 32767
integer        | integer       | 0 to 4294967295 or −2147483648 to 2147483647
bigint         | string        |
decimal        | string        |
float          | float/double  |
string         | string        | Limited length
text           | string        | Unlimited length
guid           | string        | "Globally Unique Identifier"
binary         | resource      | Limited length
blob           | resource      | Unlimited length
boolean        | boolean       | true or false
date           | date only     | \DateTime
date_immutable | date only     | \DateTimeImmutable
datetime       | date & time   | \DateTime
datetime_immutable | date & time | \DateTimeImmutable
datetimetz     | date, time, timezone | \DateTime
datetimetz_immutable | date, time, timezone | \DateTimeImmutable
time           | time only     | \DateTime
time_immutable | time only     | \DateTimeImmutable
dateinterval   | date & time difference | \DateInterval
array          | array         | serialization
simple_array   | array[string] | implode()/explode() with comma delimeter
json           | array         | json_decode()
json_array     | array         | **deprecated**
object         | object        | serialization

## Validation

### Defining rules
```php
use Symfony\Component\Validator\Constraints as Assert;

class Author
{
  /**
    * @Assert\NotBlank()
    */
  public $name;

  /**
    * @Assert\Choice(
    *  choices = { "fiction", "non-fiction" },
    *  message = "Choose a valid genre."
    * )
    */
  public $genre;

  /**
    * @Assert\NotBlank()
    * @Assert\Length(min=3)
    */
  private $firstName;
}
```

### Validator
```php
public function authorAction() {
  $author = new Author();
  // Modify new object
  $validator = $this->get('validator');
  $errors = $validator->validate($author);
  // $errors is type of ConstraintViolationList
  if (count($errors) > 0) {
    $errorsString = (string) $errors; // toString()
    return new Response($errorsString);
  }
  return new Response('The author is valid! Yes!');
}
```

### Constraints

#### Basic
- NotBlank
- Blank
- NotNull
- IsNull
- IsTrue
- IsFalse
- Type

#### String
- Email
- Length
- Url
- Regex
- Ip
- Uuid

#### Number
- Range

#### Comparison
- EqualTo
- NotEqualTo
- IdenticalTo
- NotIdenticalTo
- LessThan
- LessThanOrEqual
- GreaterThan
- GreaterThanOrEqual

#### Date
- Date
- DateTime
- Time

#### Collection
- Choice
- Collection
- Count
- UniquaEntity
- Language
- Locale
- Country

#### File
- File
- Image

#### Special
- Bic
- CardScheme
- Currency
- Luhn
- Iban
- Isbn
- Issn

#### Other
- Callback
- Expression
- All
- UserPassword
- Valid

### Targets

#### Property
> The rule is applied to `private`, `protected` or `public` field.

#### Getter
> The rule is applied to method that starts from `get`, `is` or `has`.
> Helps creating dynamic validation.

#### Class
> For custom advanced rules.