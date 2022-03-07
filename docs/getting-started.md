---
title: Getting started
date: 2022-01-18 18:06:34
slug: getting-started
---
- [What is EasyPanel](#what-is-easypanel)
- [Installation](#installation)

## What is EasyPanel

EasyPanel is a fully customizable and beautiful CRUD maker for admin panel in [Laravel](https://laravel.com) based on [Livewire](https://laravel-livewire.com).


## Installation
To install EasyPanel on your Laravel project you need to pass a few steps.

1- Install the package and its dependencies using Composer:
```shell
composer require rezaamini-ir/laravel-easypanel
```

2- Publish package files and create tables using the Artisan command:

```shell
php artisan panel:install
```

By executing this command, Laravel publishes some config and customizable files into your project directory.

One of these files is `config/easypanel.php` which is package configuration, and You can manage this file based on your needs!

Now you have to manage your administrators, and create a user as administrator to access the EasyPanel GUI!
