---
title: Fields
date: 2022-01-19 13:26:00
slug: fields
---
- [What is field](#what-is-field)
- [Define Simple Fields](#define-simple-fields)
  - [Relational Fields](#relational-fields)
- [Control Your Fields](#control-your-fields)
  - [Custom Style](#custom-style)
  - [Sortable fields](#sortable-fields)
  - [Images](#images)
    - [Clickable Images](#clickable-images)
    - [Rounded Images](#rounded-images)
    - [Width and Height](#width-and-height)
    - [Alt of Images](#alt-of-images)
  - [Badges](#badges)
    - [Rounded Badges](#rounded-badges)
    - [Badge Color](#badge-color)

## What is field
Fields are the data which have been showed in Read page!

## Define simple fields
To define the data which you want to be showed in Read page you have to manage `fields()` method on CRUD component.

This method must return an array!

For example:
```php
public function fields(){
    return [
        'name',
        'email'
    ];
}
```

With this simple array, it will call `name` and `email` property on CRUD's model.
Let's see what is happening in behind scene:
```php
$user->name

$user->email
```

**These are the properties which are available on your model, be careful!**

### Relational Fields
To call a relational value on your model, first you need to define them in your model.
Then you can call them in `fields()` method with just a point separator.

Image our model is `Article` and we have defined a `belongsTo()` relation on model class called `user`, now we can do something like this to get the name of user:
```php
public function fields(){
    return [
        'title',
        'slug',
        'user.name'
    ];
}
```
In behind scene this `.` will be rendered to `->` and the executed code is something like below:
```php
$article->user->name
```

## Control Your Fields
You may want to create more customizable fields, and add some style to them to make them more beautiful and readable.
how can You do it? Should You open the rendered CRUD files and change them in what way You want?
You it works, but after rebuilding each CRUD these changes will go away, and also they take lots of time!

There is a class called `Field` which has been imported in your CRUD components class with this namespace: `EasyPanel\Parsers\Fields\Field`.
With this class we will be able to make your fields more customizable.

Let's see an example:
```php
 public function fields(){
    return [
        'title' => Field::title('Title of article'),
    ];
}
```
The key of array is your property on model, and the value is an object of `Field::class` and you have to call the `title()` method first!

The `title` is one of the title in your Read table.

### Custom Style
You can manage the style of values in table with `style()` method.
```php
 public function fields(){
    return [
        'title' => Field::title('Title of article')->style('font-20 text-danger'),
    ];
}
```

### Sortable fields
In default, none-relational fields have sorting option, but if you want to turn it off for a dedicated field, you can easily use `withoutSorting()` method on Field object:

```php
public function fields(){
    return [
        'title' => Field::title('Title of article')->withoutSorting(),
    ];
}
```

This code will add the `class='font-20 text-danger'` attribute to each value of the title.

![](/style-example.png)

**This style is appended to table values not the head of table!**

## Images
This `Field` class allows you to work with images to make them customizable.
To show a value as an image you can use `asImage()` method, for example:

```php
public function fields(){
    return [
        'profile' => Field::title("User's profile")->asImage(),
    ];
}
```

But, You can manage your image more and more with this `Field` class.

### Clickable Images
If you want to link your images and open them directly in the browser, you can use `clickableImage()` method:

```php
public function fields(){
    return [
        'profile' => Field::title("User's profile")
                ->asImage()
                ->clickableImage(),
    ];
}
```

Also, this `clickableImage` method accepts a parameter which is the target of link and in default it is `_blank`

```php
public function fields(){
    return [
        'profile' => Field::title("User's profile")
                ->asImage()
                ->clickableImage('_self'),
    ];
}
```

### Rounded Images
You can round your image by adding `style` but there is a namespace to make it easier to you called `roundedImage()`:
```php
public function fields(){
    return [
        'profile' => Field::title("User's profile")
                ->asImage()
                ->roundedImage(),
    ];
}
```

In behind scene, it adds `rounded-circle` class to the image.

### Width and Height
You may need to change the `width` and `height` of image to show them more clearly in Read page.
It is simpler than you think, just add `width()` or `height()` method and pass them an integer for pixel!

```php
public function fields(){
    return [
        'profile' => Field::title("User's profile")
                ->asImage()
                ->roundedImage()
                ->width(60) // 60px
                ->height(100) // 100px ,
    ];
}
```
In default, the width and height are 50px.

### Alt of Images
Images are more customizable than you think!
You can pass the default alt of images, by just calling `alt()` method:

```php
public function fields(){
    return [
        'author.profile' => Field::title("Author profile")
                ->asImage()
                ->roundedImage()
                ->alt('Author profile')
    ];
}
```
**You can use the relational mode for these custom fields, like simple mode**

## Badges
A badge can make your UI much better, you can change the type of your value from simple text to a badge.

Imagine we have a model like `Article` with a `belongsTo` relation called `user`, and want to show the name of article creator in a beautiful badge:

```php
public function fields(){
    return [
        'user.name' => Field::title('Creator')
                ->asBadge(),
    ];
}
```

![](/badge.png)

### Rounded Badges
Badges can have rounded corners, to apply this rounding corner we can easily call `roundedBadge()` to make them rounded.
```php
public function fields(){
    return [
        'status' => Field::title('Article Status')
                ->roundedBadge(),
    ];
}
```

### Badge Color
Badges in EasyPanel are based on [Bootstrap](https://getbootstrap.com/docs/4.0/components/badge/) styles, and they can have about 8 colors:
- primary
- secondary
- success
- danger
- warning
- info `default`
- light
- dark

To change the type(color) of badge, we can call `badgeType($type)` method:
```php
public function fields(){
    return [
        'status' => Field::title('Article Status')
                ->roundedBadge()
                ->badgeType('primary'),
    ];
}
```

**After any change, component needs to be rebuilt!**