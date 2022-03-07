---
title: Manage Administrators
date: 2022-01-18 18:06:34
slug: manage-administrators
---
- [Authentication Strategy](#authentication-strategy)
- [Create an Administrator](#create-an-administrator)
- [Remove an Administrator](#remove-an-administrator)
- [Admin List](#admin-list)


## Authentication Strategy

There is no login or registration page to log in to your account, so to access the `/admin` route, first, you have to login into your account in the way which you want.
Then define a user as an administrator to access the EasyPanel route.

## Create an Administrator

To define a user as an administrator you have to execute this command:
```shell
php artisan panel:add [user_id]
```

_To create a super admin you can pass `--super` option to the command._

For example:

```shell
php artisan panel:add 10 --super
```

## Remove an Administrator
You can remove an administrator user with this command:
```shell
php artisan panel:remove [user_id]
```

Hint: `[user_id]` : It's the
The ID of a user that you want to make as an admin.

## Admin List

You can see the list of administrators in the command line easily:
```shell
php artisan panel:admins
```
It will show the list of administrators in the command line.

**These commands use UserProvider class in EasyPanel, and You can use your class instead of that and pass it in the config file.**

If you want to change this class, read [Admin Provider Class](/configuration#admin-provider-class) section.
