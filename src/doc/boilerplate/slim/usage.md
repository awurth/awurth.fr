---
title: Usage
type: guide
category: Slim base
order: 3
github: https://github.com/awurth/Slim
---

### Controller class
Create a new class in `src/Controller` that extends the base `Controller` class ([`src/Controller/Controller.php`](/awurth/Slim/blob/master/src/Controller/Controller.php))

``` php
// src/Controller/ArticleController.php

namespace App\Controller;

class ArticleController extends Controller
{
}
```

### Register in the container
``` php
// config/controllers.php

return [
    // ...
    'blog.article.controller' => 'App\Controller\ArticleController'
];
```

### Add a controller action
Create a method in your controller class, with the `Request` as the first argument, the `Response` as the second argument, then the route placeholders as separate arguments (and not in an `$args` array)

``` php
// src/Controller/ArticleController.php

use Slim\Http\Request;
use Slim\Http\Response;

// ...

public function getArticle(Request $request, Response $response, $id)
{
}
```

If you want the default behavior, remove the following lines from [`config/handlers.php`](/awurth/Slim/blob/master/config/handlers.php)

``` php
$container['foundHandler'] = function () {
    // ...
    
    return new RequestResponseArgs();
};
```

## Routing
You can add routes in `config/routes.php` directly or include an other routing file:

``` php
// config/routes.php

require $app->getConfigurationDir().'/routes/blog.php';
```

``` php
// src/Blog/Resources/config/routes.php
$app->group('/blog', function () {
    $this->get('/article/{id}', 'blog.article.controller:getArticle')->setName('get_blog_article');
});
```

## Templating
### Render from the controller
``` php
// src/Controller/ArticleController.php

use Slim\Http\Request;
use Slim\Http\Response;

// ...

public function getArticle(Request $request, Response $response, $id)
{
    $articles = Article::find($id);

    return $this->twig->render($response, 'blog/article/show_article.twig', [
        'article' => $article
    ]);
}
```

### Create the template
``` twig
{# templates/blog/article/show-article.twig #}

{# Extend the base layout from 'templates/layout.twig' #}
{% extends 'layout.twig' %}

{% block title %}{{ parent() }} - Blog article{% endblock %}

{% block body %}
    <div class="ui container">
        {# Display your articles here #}
    </div>
{% endblock %}
```
