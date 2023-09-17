---
layout: post
status: publish
published: true
title: Configuring My Websites
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2020-11-29 12:00:00 -0500'
date_gmt: '2020-11-29 12:00:00 -0500'
categories:
- Articles
tags: []
comments: []
---

I just migrated back to a DigitalOcean $5 droplet for some of  my websites. I wanted to do this because my homelab has minimal upload speed.

I have a "cdn" and cache on the local server. I store the files in BackBlaze.

# Install Updates & Packages

```
apt-get update
apt-get upgrade -yf
apt-get install fail2ban nginx docker-compose snapd -yf
```

# Install certbot via Snap

```
snap install core
snap refresh core
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot
snap install certbot-dns-digitalocean
```

# Request LetsEncrypt with Certbot for DigitalOcean

```
certbot certonly \
  --dns-digitalocean \
  --dns-digitalocean-credentials /root/certbot \
  --dns-digitalocean-propagation-seconds 60 \
  -d *.kvchmurphy.com \
  -d kvchmurphy.com
```
```
certbot certonly \
  --dns-digitalocean \
  --dns-digitalocean-credentials /root/certbot \
  --dns-digitalocean-propagation-seconds 60 \
  -d *.hxrsmurf.info \
  -d hxrsmurf.info
```

# NGINX config (main website)

I use Ghost blogging platform for this website and use the docker container.

```
server {
        listen 443;
        ssl on;
        ssl_certificate /etc/letsencrypt/live/kvchmurphy.com/cert.pem;
        ssl_certificate_key /etc/letsencrypt/live/kvchmurphy.com/privkey.pem;
        root /var/www/html;
        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                proxy_pass http://localhost:8080/;
        }
}
```

# NGINX config (CDN)

This config stores the cache in the directory for 30 days and has a maximum size of 18 GB. It allows NGINX to download from BackBlze "once" and then store it for X. So, I don't incur too many charges.

```
proxy_cache_path /usr/share/nginx/cache levels=1:2 keys_zone=mycache:10m max_size=18g inactive=30d use_temp_path=off;
```

```
server {
        listen 443;
        server_name cdn.kvchmurphy.com;
        ssl on;
        ssl_certificate /etc/letsencrypt/live/kvchmurphy.com/cert.pem;
        ssl_certificate_key /etc/letsencrypt/live/kvchmurphy.com/privkey.pem;
        root /var/www/html;
        location /content {
                proxy_cache mycache;
                add_header Cache-Control "public";
                add_header X-Cache-Status $upstream_cache_status;
                proxy_ignore_headers Cache-Control;
                proxy_cache_min_uses 1;
                proxy_cache_valid any 30d;
                proxy_cache_use_stale   error timeout invalid_header updating
                        http_500 http_502 http_503 http_504 http_404;
                proxy_pass [BackBlaze];
                expires 30d;
                }

                location / {
                root /usr/share/nginx/html/;
                index index.html;
                }
}
```

# Docker Compose for Ghost

```
version: '3.1'

services:
  kvchmurphy:
    image: ghost
    restart: always
    ports:
      - 8080:2368
    volumes:
      - /root/ghost/config.production.json:/var/lib/ghost/config.production.json
      - /root/ghost/content:/var/lib/ghost/content

  kvchmurphy_db:
    image: mysql
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    environment:
      MYSQL_RANDOM_ROOT_PASSWORD: "yes"
      MYSQL_DATABASE: ghost
      MYSQL_USER: ghost
      MYSQL_PASSWORD: [redacted]
```