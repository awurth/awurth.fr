---
title: Installation
type: guide
category: Silex User Bundle
order: 2
---

## Download Silex User Bundle using Composer
Require the bundle with Composer:
``` bash
$ composer require awurth/silex-user
```

## Register the Service Provider
Register the provider in the container:
``` php
$app->register(new AWurth\Silex\User\Provider\SilexUserServiceProvider());
```
## Create your User class
The goal of this bundle is to persist a `User` class to a database. Your first job, then, is to create the `User` class for your application. This class can look and act however you want: add any properties or methods you find useful.

The bundle provides a base class that is already mapped for most fields to make it easier to create your entity. You just have to extend the base `User` class from the `Entity` folder.

### Doctrine ORM User class
``` php
<?php

namespace App\Security\Entity;

use AWurth\Silex\User\Entity\User as BaseUser;
use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity
 * @ORM\Table(name="`user`")
 */
class User extends BaseUser
{

}
```

### Doctrine MongoDB ODM User class
``` php
<?php

namespace App\Security\Document;

use AWurth\Silex\User\Document\User as BaseUser;
use Doctrine\ODM\MongoDB\Mapping\Annotations as ODM;

/**
 * @ODM\Document(collection="user")
 */
class User extends BaseUser
{

}
```

## Configure your application's security
In order to use the User Provider with Symfony's security component, you will have to create at least one firewall with an authentication method (login form, http basic, ...) and a user provider.
Below is an example of the configuration using a login form:
``` php
$app['security.role_hierarchy'] = [
    'ROLE_ADMIN' => [
        'ROLE_USER',
        'ROLE_ALLOWED_TO_SWITCH'
    ]
];

$app['security.firewalls'] = [
    'main' => [
        'pattern' => '^/',
        'form' => [
            'login_path' => '/login',
            'check_path' => '/login_check',
            'with_csrf' => true
        ],
        'logout' => [
            'logout_path' => '/logout',
            'invalidate_session' => true
        ],
        'anonymous' => true,
        'users' => function ($app) {
            return $app['silex_user.user_provider.username'];
        }
    ]
];
```
The `with_csrf` option is optional. If set to `true`, the bundle will protect the login form with a CSRF token.

For more info on how to configure your application's security, check out the [documentation](https://silex.symfony.com/doc/2.0/providers/security.html).

## Configure the bundle
Before you can use the provider, you need to set three options:
- `object_manager`: The name of the Doctrine ObjectManager in your application's container
- `firewall_name`: The name of the firewall that you configured in the previous step
- `user_class`: The fully qualified class name of your `User` class
``` php
$app['silex_user.options'] = [
    'object_manager' => 'orm.em',
    'firewall_name' => 'main',
    'user_class' => 'App\Security\Entity\User'
];
```

## Update your database schema
If your application has a command line tool to update your database schema, you can run the following command:
``` bash
$ your_command_line_tool doctrine:schema:update --force
```

If not, you can import the `user.sql` file (`vendor/awurth/silex-user/user.sql`) in your DBMS (MySQL)
