---
title: Inputs
date: 2022-01-18 18:06:34
slug: inputs
---
- [Provide Inputs](#provide-inputs)
- [Simple inputs](#provide-inputs)
    - [Available Types](#available-types)
- [Inputs, but pro!](#inputs-but-pro)
    - [Text](#text)
    - [Placeholder](#placeholder)
    - [Input custom style](#input-custom-style)
    - [Autocomplete input](#autocomplete-input)
    - [Input Mode](#input-mode)

## Provide Inputs

To provide inputs, you must define them into your CRUD component which has been located in `app/CRUD/` directory.

There is a method called `inputs()` which allows you to define crud inputs for Create and Update page!

## Simple inputs

You can easily pass your model property as key and input name as value to make a simple input for your CRUD.
For example:

```php
public function inputs(){
    return [
        'name' => 'text',
        'image' => 'file',
        'email' => 'email',
        'active' => 'checkbox',
        'expire_time' => 'datetime',
        'birth_day' => 'date',
        'notify_time' => 'time',
        'status' => ['select' => [
            'accepted' => 'Accepted :)',
            'rejected' => 'Rejected :(',
            'pending' => 'Pending!',
        ]],
    ];
}

```

And that's it! This code will generate a simple form which includes 4 inputs.

#### Available types

- Ckeditor
- Checkbox
- Text
- Select
- File
- Password
- Number
- Email
- Date
- Datetime
- Time
- Textarea


## Inputs, but pro!
You can create inputs as simple as possible as you want, but there is more customizibility to make more better inputs!

**All of these inputs have `EasyPanel\Parsers\HTMLInputs` namespace and start with label() method as a static method**

### Text

```php
public function inputs(){
    return [
        'title' => Text::label('Title of Article')
    ];
} 
```

### Placeholder

```php
public function inputs(){
    return [
        'title' => Text::label('Title of Article')
            ->placeholder('Please enter the title of article...')
    ];
}
```
### Input custom style

```php
public function inputs(){
    return [
        'title' => Text::label('Title of Article')
            ->inputStyle('border border-primary')
    ];
} 
```

### Autocomplete input

In default, the `autocomplete` attribute is set to `on`, but you can turn it off.

```php
public function inputs(){
    return [
        'title' => Text::label('Title of Article')
            ->inputStyle('border border-primary')
            ->withoutAutocomplete()
    ];
} 
```

Or, there is a replacement for `withoutAutocomplete` called `withoutAutofill`:

```php
public function inputs(){
    return [
        'email' => Email::label('Email')
            ->placeholder("User's email...")
            ->inputStyle('border border-primary')
            ->withoutAutofill()
    ];
} 
```

### Input Mode

Livewire has 3 different mode for its inputs:

- wire:model
- wire:model.lazy
- wire:model.deffer

And you can create your inputs based on your needs, for example you want to use different modes for each input you can do it easy:

```php
public function inputs(){
    return [
        'expired_at' => Datetime::label('Expiration time')
                        ->lazyMode(), // it will use wire:model.lazy in input
        
        'name' => Text::label('Name')
                    ->defferMode() // it will use wire:model.deffer in input
    ];
} 
```

**If you don't pass anything, it will decide based on your config file and `easy_panel.lazy_mode` key, if it is `true` all of inputs will render by `wire:model.lazy` and if it is `false` all of them will render by `wire:model`.**

##### Input classes list:
- `EasyPanel\Parsers\HTMLInputs\Text`
- `EasyPanel\Parsers\HTMLInputs\Ckeditor`
- `EasyPanel\Parsers\HTMLInputs\Checkbox`
- `EasyPanel\Parsers\HTMLInputs\Select`
- `EasyPanel\Parsers\HTMLInputs\File`
- `EasyPanel\Parsers\HTMLInputs\Password`
- `EasyPanel\Parsers\HTMLInputs\Number`
- `EasyPanel\Parsers\HTMLInputs\Email`
- `EasyPanel\Parsers\HTMLInputs\Date`
- `EasyPanel\Parsers\HTMLInputs\Datetime`
- `EasyPanel\Parsers\HTMLInputs\Time`
- `EasyPanel\Parsers\HTMLInputs\Textarea`