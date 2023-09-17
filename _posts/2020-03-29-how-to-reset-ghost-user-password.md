---
layout: post
status: publish
published: true
title: How To Reset Ghost User Password
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2020-03-29 12:00:00 -0500'
date_gmt: '2020-03-29 12:00:00 -0500'
categories:
- Tutorial
tags: []
comments: []
---

Per [Farmsoft Studios](https://www.farmsoftstudios.com/blog/2014/01/web-applications/resetting-your-ghost-blog-password/) and [SoftHints](https://blog.softhints.com/how-to-reset-user-password-ghost-blog-mysql/), one can follow the steps below:

1. Generate Bcrypt hash from [PasswordHashing](https://passwordhashing.com/BCrypt)
2. Get the ghost config password (database access)

```
cd /var/www/ghost
ghost config get database.connection.password
```

3. Login to mysql and execute the code below (replacing with hash and respective user's e-mail)

```
mysql -u [ghost] -p
use my_ghost_base;
select * from users;
UPDATE users SET password='[PASTE_HASH_HERE]' WHERE email = '[YOUR_EMAIL_ADDRESS]';
exit
```

4. Login to Ghost with the new password

5. Reset your user's password


