---
title: Component Structure
date: 2022-01-18 18:06:34
slug: component-structure
---
- [What is the component](#what-is-the-component)
- [How to create a component](#how-to-create-a-component)
- [Component Methods](#component-methods)
    - [Actions](#actions)
    - [Model for Component](#model-for-component)
    - [Fields](#fields)
    - [Searchable](#searchable)
        - [Lazy Mode for Searching](#laze-mode-for-searching)
        - [Disable Searching](#disable-searching)
    - [Inputs](#inputs)
    - [Validation](#validation)
    - [Store Files](#store-files)
- [Build CRUD](#build-crud)

## What is the component
Components in EasyPanel are the classes that have been located in the `app/CRUD` directory, and You can manage your CRUDs by editing these components!

To have CRUD action for our models, each of them must have a single component in `app/CRUD`.

## How to create a component

To create a CRUD for your models, you can easily go to the `/admin` route (this address can be modified in the config file), then open the `CRUD Manager` page.
Now you can manage or create new CRUDs.

There is a button called `Create CRUD`, after opening this page a form will be shown, and You can pass your model namespace, CRUD's route, and CRUD's icon.
After creating the CRUD with the `create` button, a new file will be created in the `app/CRUD` directory which has this format:
```php 
ModelComponent.php // Model is your model name
```

## Component Methods

Each component has a few methods and properties to be managed by them.

### Actions

As you may know, CRUD stands for 4 words:
- Create
- Read
- Update
- Delete

3 of these actions are manageable in CRUD components, and you can manage them easily in properties:
```php
public $create = true;
public $delete = true;
public $update = true;
```
If you want to turn one of them off, you can set it as `false`, that's it!

### Model for Component
As was said before, each CRUD component must have a model.
This model will be parsed automatically after creating a CRUD component on the CRUD Manager page.
If You want to change this model for any reason *(is not recommended!)*, you can pass a new model in the `getModel()` component method:

```php 
public function getModel()
{
    return Article::class;
}
```

**This Method must return a model namespace!**

### Fields

We have documented a lot about Fields in [Field Page](/fields).

### Searchable

As you may be noticed, there is a feature in EasyPanel to search on our model data and its relations.

To define the searchable fields, you can return an array with some properties which are available on model properties:
```php
public function searchange(){
    return ['title', 'content'];
}
```

To search in relational values, first you must define the relationship in your model, then:
```php
public function searchange(){
    return ['title', 'content', 'user.name', 'user.email'];
}
```
These `.` will be replaced by `->` in behind scene, take care about the values and properties and their existence.


#### Laze Mode for Searching

If you want to use lazy mode for your searching strategy, to decrease pressure on your server you can change the `lazy_mode` key on your config file in the `config/easy_panel.php` directory:
```php

return [
    ... 
    'lazy_mode' => true,
    ...
];
 
```

In behind scene, It will use `wire:model.lazy` instead of `wire:model`.

#### Disable Searching

To turn the searching feature off, You can return an empty array in the `searchable()` method:

```php
public function searchange(){
    return [];
}
```

### Inputs
We have documented a lot about Inputs in [Inputs Page](/inputs).

### Validation
Validation rules in EasyPanel components uses the [default validation in Laravel](https://laravel.com/docs/master/validation).
To use validation you need to return an array with keys and values in the `validationRules()` method in the CRUD component:

```php
public function validationRules()
{
    return [
        'title' => 'required|min:2|max:255',
        'content' => 'required|min:30'
    ];
} 
```

**The key should be matched with the key of inputs!**

### Store Files

If you use inputs with file type, You may be wondering how can you change the path of the store method?

It's really easy in EasyPanel:
```php
public function storePaths()
{
    return [
        'profile' => 'photos/profile-photo'
    ];
} 
```

In behind scene it will do something like this:
```php
$this->profile->store('photos/profile-photo'); 
```

The `store()` method belong to Livewire, [Read more about store()](https://laravel-livewire.com/docs/2.x/file-uploads#basic-upload).

**The key must be equal to the input key.**

## Build CRUD
When you make the CRUD Component customize based on your needs.
You need to build or rebuild the CRUD on the `CRUD Manager` Page.

It will create 2 new directories for your project in `app/Http/Livewire/Admin` and `resources/views/livewire/admin/` with the name of your model!

These 2 folders contain CRUD components, and you can customize them based on your needs.

For example, if our model is `Article` we will have these components:

```
app/Http/Livewire/Admin/Article:
│─── Create.php
│─── Read.php 
│─── Single.php 
│─── Update.php 

resources/views/livewire/admin/article:
│─── create.blade.php
│─── read.blade.php 
│─── single.blade.php 
│─── update.blade.php 
```

Be careful, when you rebuild a CRUD all components will be rebuilt again, and every custom change will be removed!

**Any changes in validationRules(), storePaths(), inputs(), fields() and getModel() need rebuilt!**
