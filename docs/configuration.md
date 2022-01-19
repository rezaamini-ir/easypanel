---
title: Configuration
date: 2022-01-18 18:06:34
slug: configuration
---
- [How to Manage Configuration](#how-to-manage-configuration)
- [Disable/Enable Module](#disableenable-module)
- [RTL Mode](#rtl-mode)
- [Changing Language](#changing-language)
- [User Model](#user-model)
- [Authentication Guard](#authentication-guard)
- [Unauthorized Redirect Path](#unauthorized-redirect-path)
- [Routes Prefix](#routes-prefix)
- [Additional Middlewares](#additional-middlewares)
- [Pagination Count](#pagination-count)
- [Lazy Updating](#lazy-updating)
- [Change Auth Strategy](#change-auth-strategy)
- [Admin Provider Class](#admin-provider-class)

## How to Manage Configuration

When you run `panel:install` command, it will publish the config file in `config/easy_panel.php` path, and You can manage it easily.

### Disable/Enable Module
It's possible to disable or enable whole module easily by just changing the `enable` key in config file.
```php 
return [
    ...
    'enable' => true,
    ...
];
```
When you set `enable` as `false` the routes won't be registered anymore, and you can't access the routes to manage your Admin Panel!

### RTL Mode
If you want to change your style from LTR to RTL You can change the value of `rtl_mode` in configs:

```php 
return [
    ...
    'rtl_mode' => true,
    ...
];
```

## Changing Language
EasyPanel is fully translatable, to manage the values and texts, You can copy the `resources/lang/en_panel.json` file and customize the texts.

For example if You want to add a `france` language to EasyPanel, You have to create a copy from `resources/lang/en_panel.json` into `resources/lang/fr_panel.json`, now You can set the value of `lang` to `fr`.

Don't need to pass full name of file, just pass the prefix before `_panel.json`

The pattern is: `*_panel.json`: 

- fa_panel.json => fa
- en_panel.json => en
- chinese_panel.json => chinese

```php 
return [
    ...
    'lang' => 'chinese',
    ...
];
```

### User Model

EasyPanel to manage admins uses default `User` Model, if You want to change it, You can pass new model into `user_model` config key.

```php 
return [
    ...
    'user_model' => \App\Models\Admin::class,
    ...
];
```

### Authentication Guard

In default EasyPanel uses the `web` guard to identify the logged-in user.

If you have customized this, or You need to change the guard for authentication, You have to change `auth_guard` in config:


```php 
return [
    ...
    'auth_guard' => 'admin',
    ...
];
```

### Unauthorized Redirect Path

If an unauthorized user tries to access the EasyPanel routes, it will be redirected to a path, and this path can be changed in config file with `redirect_unauthorized` key.

```php 
return [
    ...
    'redirect_unauthorized' => '/',
    ...
];
```

### Routes Prefix

In default, EasyPanel uses `/admin` prefix, and You can access the routes by : `localhost:8000/admin`.

As you may guess, It's fully customizable in config file:

```php 
return [
    ...
    'route_prefix' => 'panel', // localhost:8000/panel
    ...
];
```

### Additional Middlewares

If you need to add more middlewares to EasyPanel routes, you can pass them in config as an array:

```php 
return [
    ...
    'additional_middlewares' => ['AdminHasApproved', 'UserIsNotBlocked']
    ...
];
```

### Pagination Count

The Read page has a pagination, and You can customize the count of pagination in the config.

The default is 20, and You can change it:
```php 
return [
    ...
    'pagination_count' => 30,
    ...
];
```

### Lazy Updating

Lazy mode uses `wire:model.lazy` in searching strategy, and inputs instead of `wire:model`.

[Read more about lazy updating](https://laravel-livewire.com/docs/2.x/properties#lazy-updating). 

```php 
return [
    ...
    'lazy_mode' => true,
    ...
];
```

**It will accept a boolean value.**

### Change Auth Strategy

Admin Identifier class uses a Facade, and You can change the base class very easily.

For example, if You want to change strategy of identifying administrators, You can create a class with a public `check($id)` method:

```php
namespace App\Services\Auth;

class AdminIdentifier {

    public function check($id){
        return \App\Models\Admin::where('user_id', $id)->exists();
    }
} 
 
```

Now You can pass the new namespace into the config with `auth_class` key:

```php 
return [
    ...
    'auth_class' => App\Services\Auth\AdminIdentifier::class,
    ...
];
```

### Admin Provider Class

Admin Provider class also uses a Facade, and You can swap the class.

If you need to customize the way of creating an administrator, delete an administrator or administrator lists, You have to create a custom class and change the value of `admin_provider_class` to new class.

This class must have 4 methods called:

- `makeAdmin($id, $isSuper = true): array`
- `getAdmins(): array|collection`
- `findUser(): Model`
- `deleteAdmin(): void`



```php
namespace App\Services;

class AdminProvider {

    public function makeAdmin($id, $isSuper = true){
        try{
            \App\Models\Admin::create(['user_id' => $id, 'super_user' => $isSuper]);
            return [
                'type' => 'success',
                'message' => 'Admin created!'
            ];
        } catch(\Exception $exception){
            return [
                'type' => 'error',
                'message' => $exception->getMessage()
            ];
        }
    }
    
    public function getAdmins(){
        return \App\Models\User::whereHas('admin')->get();
    }
    
    public function findUser($id){
        return \App\Models\User::findOrFail($id);
    }
    
    public function deleteAdmin($id){
        \App\Models\Admin::where('user_id', $id)->delete();
    }
    
} 
 
```

Now You can pass the new namespace into the config with `admin_provider_class` key:

```php 
return [
    ...
    'admin_provider_class' => App\Services\AdminProvider::class,
    ...
];
```