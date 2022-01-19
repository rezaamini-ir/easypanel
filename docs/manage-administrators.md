---
title: Manage Administrators
date: 2022-01-18 18:06:34
slug: manage-administrators
---

## Authentication Strategy

There is no login or registration page to logging in to your account, so to access the `/admin` route, first you have to login into your account in the way which you want.
Then define a user as administrator to access the EasyPanel route.

## Create an administrator

To define a user as administrator you have to execute this command:
```shell
php artisan panel:add [user_id]
```

_To create a super admin you can pass `--super` option to the command._

For example:

```shell
php artisan panel:add 10 --super
```

## Remove an administrator
You can remove an administrator user with this command:
```shell
php artisan panel:remove [user_id]
```

Hint: `[user_id]` : It's the
ID of user that you want to make as an admin.

**These commands use UserProvider class in EasyPanel, and You can use your own class instead of that and pass it in config file.**