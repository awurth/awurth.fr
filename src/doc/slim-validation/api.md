---
title: API
type: guide
category: Slim Validation
order: 3
---

## Validator

### __construct( [ bool $storeErrorsWithRules = true [, array $defaultMessages = [] ]] )
Creates a new Validator instance.

#### Arguments
* *(Optional)* `$storeErrorsWithRules` **bool**
    *default* **true**

    * If set to `true`, errors will be stored in an associative array with the validation rules names as the key
    * If set to `false`, errors will be stored in an array of strings

* *(Optional)* `$defaultMessages` **array**
    *default* **array()**

    An array of messages to overwrite the default [Respect Validation](https://github.com/Respect/Validation) messages

#### Usage
``` php
// With the default configuration
$validator = new Validator();

// With custom default messages
$validator = new Validator(true, [
    'length' => 'Custom message for "length" rule',
    'notBlank' => 'Custom message for "notBlank" rule'
]);
```
### validate( Request $request, array $rules [, array $messages = [] ] )
Validates request parameters with the given validation rules.

#### Arguments
* `$request` **Psr\Http\Message\ServerRequestInterface**

    The `$request` object from your route callback

* `$rules` **array**

    An array of validation rules associated to request parameters

* *(Optional)* `$messages` **array**
    *default* **array()**

    An array of messages to overwrite [Respect Validation](https://github.com/Respect/Validation) and [default rules messages](index.html#defaultMessages) for the given validation rules

#### Return *Validator*

#### Usage
See [Slim Validation Usage](usage.html).

### isValid( )
Tells if there is no error.

#### Return *bool*

### getErrors( )
Gets all errors.

#### Return *array*

### getFirstError( string $param )
Gets the first error of a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

#### Return *string*

### getParamErrors( string $param )
Gets all errors of a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

#### Return *array*

### getParamRuleError( string $param, string $rule )
Gets the error message of a request parameter for the given validation rule.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$rule` **string**

    The validation rule's name

#### Return *string*

### getData( )
> *@deprecated* since version 2.1, will be removed in 3.0. Use `getValues()` instead.

Gets the validated data.

#### Return *array*

### getValue( string $param )
Gets the value of a request parameter in validated data.

#### Arguments
* `$param` **string**

    The request parameter's name

#### Return *mixed*

### addError( string $param, string $message )
Adds an error message for a request parameter. Useful if you want to add a message without using the validate method.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$message` **string**

    The error message

#### Return *Validator*

### addErrors( string $param, array $messages )
> *@deprecated* since version 2.1, will be removed in 3.0.

Adds error messages for a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$messages` **array**

    An array of error messages

#### Return *Validator*

### setErrors( array $errors )
Sets errors (overwrites all errors).

#### Arguments
* `$errors` **array**

    An array of error messages
    ``` php
    $errors = [
        'username' => [
            'length' => 'Message for "length" rule',
            'alnum' => 'Message for "alnum" rule'
        ],
        'password' => [
            'Bad password'
        ]
    ];
    ```

### setParamErrors( string $param, array $errors )
Sets the errors of a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$errors` **array**

    An array of error messages. It can be an array of strings or an associative array with the validation rules names as the keys

#### Return *Validator*

### setValues( array $data )
> Replaced by `setValues()` and `addValue()` in version 3.0.

Merges the validated data with `$data`.

#### Arguments
* `$data` **array**

    An associative array with the request parameters names as the keys and their value as the values
    ``` php
        $data = [
            'username' => 'Alexis',
            'password' => 'my_password'
        ];
    ```

#### Return *Validator*

## Twig Extension
