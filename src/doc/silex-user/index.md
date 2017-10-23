---
title: Introduction
type: guide
category: Silex User Bundle
order: 1
github: https://github.com/awurth/silex-user
---

The Symfony Security component provides a flexible security framework that allows you to load users from configuration, a database, or anywhere else you can imagine. The Silex User Bundle builds on top of this to make it quick and easy to store users in a database.

Features include:

- Users can be stored via Doctrine ORM or MongoDB ODM
- Registration support, with an optional confirmation per email
- Unit tested

Inspired by the [FOS User Bundle](https://github.com/FriendsOfSymfony/FOSUserBundle).

See [awurth/silex](https://github.com/awurth/silex) for an example implementation.

## Prerequisites
- Silex 2.x
- [Service Controller Service Provider](https://silex.symfony.com/doc/2.0/providers/service_controller.html)
- [Twig Service Provider](https://silex.symfony.com/doc/2.0/providers/twig.html)
- [Session Service Provider](https://silex.symfony.com/doc/2.0/providers/session.html)
- [Translation Service Provider](https://silex.symfony.com/doc/2.0/providers/translation.html)
- [Validator Service Provider](https://silex.symfony.com/doc/2.0/providers/validator.html)
- [Form Service Provider](https://silex.symfony.com/doc/2.0/providers/form.html)
- [Security Service Provider](https://silex.symfony.com/doc/2.0/providers/security.html)
- Any Doctrine ORM or ODM provider
    - [Doctrine ORM Service Provider](https://github.com/dflydev/dflydev-doctrine-orm-service-provider)
    - [Doctrine MongoDB ODM Provider](https://github.com/saxulum/saxulum-doctrine-mongodb-odm-provider)

### Optional
- A Doctrine Manager Registry provider (if you want to use the default validation rules which use the `UniqueEntity` validation constraint)
    - [Doctrine ORM Manager Registry Provider](https://github.com/saxulum/saxulum-doctrine-orm-manager-registry-provider)
    - [Doctrine MongoDB ODM Manager Registry Provider](https://github.com/saxulum/saxulum-doctrine-mongodb-odm-manager-registry-provider)

- [SwiftMailer Service Provider](https://silex.symfony.com/doc/2.0/providers/swiftmailer.html) for email activation
