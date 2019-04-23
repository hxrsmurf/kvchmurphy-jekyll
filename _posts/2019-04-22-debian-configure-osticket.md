---
layout: post
status: publish
published: true
title: Setup OS Ticket on Debian 9.8
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2019-04-22 19:08:00 -0500'
date_gmt: '2019-04-22 19:08:00 -0500'
categories:
- Tutorial
tags: []
comments: []
---

This is how I configured OS Ticket on `Debian 9.8`. 

```
Distributor ID: Debian
Description:    Debian GNU/Linux 9.8 (stretch)
Release:        9.8
Codename:       stretch
```

#### Use `apt-get install` to install some packages

```   
apt-get install apache2 mysql-server net-tools php php php-apcu php-imap php-intl php-mbstring php-mysql php-xml php7.0-gd postfix unzip -yf
```

#### Create MySQL Database and Username
```
create database osticket;
CREATE USER 'osticket'@'localhost' IDENTIFIED BY 'YourPasswordHere';
GRANT ALL PRIVILEGES ON osticket.* TO 'osticket'@'localhost';
```

#### Download, Unzip, and Copy OS Ticket  

- [OS Ticket](https://osticket.com/download/)
- unzip osTicket-v1.11.zip
- cp -r upload/ /var/www/html/osticket


#### Change to the directory and modify permissions

- cd /var/www/html/osticket
- chmod -R 775 *
- chown -R www-data:www-data *

#### Copy the sample configuration, modify its permissions

```
cd /var/www/html/osticket
cp include/ost-sampleconfig.php include/ost-config.php
chmod 0666 include/ost-config.php
```

#### Configure OS Ticket at your website

- [Installation Guide](https://docs.osticket.com/en/latest/Getting%20Started/Installation.html)

#### Clean Up After Installation & Configuration

- cd /var/www/html/osticket
- rm -rf setup/
- chmod 644 include/ost-config.php

#### Configure Postfix To Use Gmail As SMTP Relay

- [Gmail SMTP Relay](https://support.google.com/a/answer/2956491?hl=en)

```
nano /etc/postfix/main.cf
relayhost = [smtp-relay.gmail.com]:587
```

#### OS Ticket URL Examples

- [Agent](http://www.yourdomain.com/support)
- [User](http://www.yourdomain.com/support/scp)