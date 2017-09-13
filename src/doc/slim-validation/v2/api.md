---
title: API
type: guide
category: Slim Validation
version: 2
order: 3
---

## Validator

### __construct( [ $storeErrorsWithRules [, $defaultMessages ]] )
Creates a new Validator instance.

#### Arguments
* *(Optional)* `$storeErrorsWithRules` **bool**
    *default* **true**

    * If set to `true`, errors will be stored in an associative array with the validation rules names as the key
    * If set to `false`, errors will be stored in an array of strings

* *(Optional)* `$defaultMessages` **array**
    *default* **array()**

    An array of messages to overwrite the default [Respect Validation](https://github.com/Respect/Validation) messages. See [setDefaultMessages()](#setDefaultMessages-messages)

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
### validate( $request, $rules [, $messages ] )
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

### getFirstError( $param )
Gets the first error of a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

#### Return *string*

### getParamErrors( $param )
> Replaced by `getErrors()` in version 3.0.

Gets all errors of a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

#### Return *array*

### getParamRuleError( $param, $rule )
> Replaced by `getError()` in version 3.0.

Gets the error message of a request parameter for the given validation rule.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$rule` **string**

    The validation rule's name

#### Return *string*

### getData( )
> *@deprecated* since version 2.1, will be removed in 3.0. Use `getValues()` instead.

#### Return *array*

### getValues( )
Gets the validated data.

#### Return *array*

### getValue( $param )
Gets the value of a request parameter in validated data.

#### Arguments
* `$param` **string**

    The request parameter's name

#### Return *mixed*

### addErrors( $param, $messages )
> *@deprecated* since version 2.1, will be removed in 3.0. Use addError() instead.

Adds error messages for a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$messages` **array**

    An array of error messages

#### Return *Validator*

### addError( $param, $message )
Adds an error message for a request parameter. Useful if you want to add a message without using the validate method.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$message` **string**

    The error message

#### Return *Validator*

### setDefaultMessages( $messages )
Sets default error messages.

#### Arguments
* `$messages` **array**

    An array of error messages associated to validation rules names
    ``` php
    $messages = [
        'length' => 'This field must have a length between {{minValue}} and {{maxValue}} characters',
        'notBlank' => 'This field is required'
    ];
    ```

#### Return *Validator*

### setDefaultMessage( $rule, $message )
Sets default error messages.

#### Arguments
* `$rule` **string**

    The validation rule name

* `$message` **string**

    The error message

#### Return *Validator*

### setErrors( $errors )
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

### setParamErrors( $param, $errors )
> Replaced by `setErrors()` in version 3.0.

Sets the errors of a request parameter.

#### Arguments
* `$param` **string**

    The request parameter's name

* `$errors` **array**

    An array of error messages. It can be an array of strings or an associative array with the validation rules names as the keys

#### Return *Validator*

### setValues( $data )
> Replaced by `setValues()` and `setValue()` in version 3.0.

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

### has_errors( )
Tells if the validator contains errors.

#### Return *bool*

### has_error( param )
Tells if there is an error message for the given request parameter.

#### Arguments
* `param` **string**

    The request parameter's name

#### Return *bool*

### error( param )
Gets the first error message for the given request parameter.

#### Arguments
* `param` **string**

    The request parameter's name

#### Return *string*

### errors( [ param ] )
Gets all errors.

#### Arguments
* *(Optional)* `param` **string**

    The request parameter's name. If specified, the function will only return errors of this parameter

#### Return *array*

### val( param )
Gets the value of a request parameter in validated data. Can be used to set the `value=""` html attribute after submitting a form that contains errors.

#### Arguments
* `param` **string**

    The request parameter's name

#### Return *mixed*
