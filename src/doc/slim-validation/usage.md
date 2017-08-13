---
title: Usage
type: guide
category: Slim Validation
order: 2
---

## Basic usage

``` php
use Respect\Validation\Validator as V;

// The validate method returns the validator instance
$validator = $container->validator->validate($request, [
    'get_or_post_parameter_name' => V::length(6, 25)->alnum('_')->noWhitespace(),
    // ...
]);

if ($validator->isValid()) {
    // Do something...
} else {
    $errors = $validator->getErrors();
}
```

## Custom messages
Slim Validation allows you to set custom messages for validation errors. There are 4 types of custom messages:

### Default rules messages
The ones defined in the `Validator` constructor.

### Global rules messages
Messages that overwrite [Respect Validation](https://github.com/Respect/Validation) and [default rules messages](index.html#defaultMessages) when calling the `validate` method.

``` php
$container->validator->validate($request, [
    'get_or_post_parameter_name' => V::length(6, 25)->alnum('_')->noWhitespace(),
    // ...
], [
    'length' => 'Custom message',
    'alnum' => 'Custom message',
    // ...
]);
```

### Individual rules messages
Messages for a single request parameter. Overwrites all above messages.

``` php
$container->validator->validate($request, [
    'get_or_post_parameter_name' => [
        'rules' => V::length(6, 25)->alnum('_')->noWhitespace(),
        'messages' => [
            'length' => 'Custom message',
            'alnum' => 'Custom message',
            // ...
        ]
    ],
    // ...
]);
```

### Single parameter messages
Defines a single error message for a request parameter, ignoring the validation rules. Overwrites all messages.

``` php
$container->validator->validate($request, [
    'get_or_post_parameter_name' => [
        'rules' => V::length(6, 25)->alnum('_')->noWhitespace(),
        'message' => 'This field must have a length between 6 and 25 characters and contain only letters and digits'
    ],
    // ...
]);
```

## Twig extension
This package comes with a Twig extension to display error messages and submitted values in your Twig templates. You can skip this step if you don't want to use it.

To use the extension, you must install twig first
``` bash
$ composer require slim/twig-view
```

**See the [API](api.html#Twig-Extension) for available features**

### Configuration
``` php
$container['view'] = function ($container) {
    // Twig configuration
    $view = new Slim\Views\Twig(...);
    // ...

    // Add the validator extension
    $view->addExtension(
        new Awurth\SlimValidation\ValidatorExtension($container['validator'])
    );

    return $view;
};
```

## Example
##### AuthController.php
``` php
public function register(Request $request, Response $response)
{
    if ($request->isPost()) {
        $this->validator->validate($request, [
            'username' => V::length(6, 25)->alnum('_')->noWhitespace(),
            'email' => V::notBlank()->email(),
            'password' => V::length(6, 25),
            'confirm_password' => V::equals($request->getParam('password'))
        ]);

        if ($this->validator->isValid()) {
            // Register user in database
            return $response->withRedirect('url');
        }
    }

    return $this->view->render($response, 'register.twig');
}
```

##### register.twig
``` twig
<form action="url" method="POST">
    <input type="text" name="username" value="{{ val('username') }}">
    {% if has_error('username') %}<span>{{ error('username') }}</span>{% endif %}

    <input type="text" name="email" value="{{ val('email') }}">
    {% if has_error('email') %}<span>{{ error('email') }}</span>{% endif %}

    <input type="text" name="password">
    {% if has_error('password') %}<span>{{ error('password') }}</span>{% endif %}

    <input type="text" name="confirm_password">
    {% if has_error('confirm_password') %}<span>{{ error('confirm_password') }}</span>{% endif %}
</form>
```
