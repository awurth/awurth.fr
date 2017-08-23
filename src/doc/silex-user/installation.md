---
title: Installation
type: guide
category: Silex User
order: 2
---

## Download SilexUser using Composer
Require the provider with Composer
``` bash
$ composer require awurth/silex-user
```

## Register the Service Provider
Register the provider in the container
``` php
$app->register(new AWurth\SilexUser\Provider\SilexUserServiceProvider());
```
## Create your User class
The goal of this provider is to persist a `User` class to a database. Your first job, then, is to create the `User` class for your application. This class can look and act however you want: add any properties or methods you find useful.

SilexUser provides a base class that is already mapped for most fields to make it easier to create your entity. You just have to extend the base `User` class from the `Entity` folder.

``` php
<?php

namespace Security\Entity;

use AWurth\SilexUser\Entity\User as BaseUser;
use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity
 * @ORM\Table(name="`user`")
 */
class User extends BaseUser
{

}
```

## Configure your application's security
In order to use the User Provider with Symfony's security component, you will have to create at least one firewall with an authentication method (login form, http basic, ...) and a user provider.
Below is an example of the configuration using a login form
``` php
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
        'users' => $app['silex_user.user_provider.username']
    ]
];
```
The `with_csrf` option is optional. If set to `true`, SilexUser will protect the login form with a CSRF token.

For more infos on how to configure your application's security, check out the [documentation](https://silex.symfony.com/doc/2.0/providers/security.html).

## Configure SilexUser
Before you can use the provider, you need to set a two options
- `firewall_name`: The name of the firewall that you configured in the previous step
- `user_class`: The fully qualified class name of your `User` class
``` php
$app['silex_user.options'] = [
    'firewall_name' => 'main',
    'user_class' => 'Security\Entity\User'
];
```
