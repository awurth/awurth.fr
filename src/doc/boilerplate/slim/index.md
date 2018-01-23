---
title: Installation
type: guide
category: Slim base
order: 1
github: https://github.com/awurth/slim-base
---

### Create project using Composer
``` bash
$ composer create-project awurth/slim-base [project-name]
```

### Download Bower and npm dependencies
``` bash
$ npm install
```

This will create a `lib/` folder in `public/` for jQuery and Semantic UI

#### Install Gulp globally
``` bash
$ npm install -g gulp-cli
```

#### Run watcher to compile SASS and Javascript
``` bash
$ gulp
```

You may have to edit the files in `src/App/Resources/assets/` while running gulp for the first time to generate the static `css` and `js` files

### Setup permissions
You will have to give write permissions to the `cache/` folder

``` bash
$ chmod 777 cache/twig
```

### Create tables
After creating a database with the name you set during the installation (or manually in `bootstrap/parameters.yml`), create tables by executing the `bootstrap/database.php` file

``` bash
$ php bootstrap/database.php
```
