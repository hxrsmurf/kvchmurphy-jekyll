---
layout: post
status: publish
published: true
title: GitLab - Install & Configure URL
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2021-06-27 12:00:00 -0500'
date_gmt: '2021-06-27 12:00:00 -0500'
categories:
- Tutorial
tags: []
comments: []
---

[Debian Install Docs](https://about.gitlab.com/install/#debian)

```
apt-get update
apt-get install -y curl openssh-server ca-certificates perl
apt-get install -y postfix
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | bash
EXTERNAL_URL="http://gitlab.hxrmsmurf.info" apt-get install gitlab-ee
```

[Update External URL](https://stackoverflow.com/questions/19456129/how-do-we-change-the-url-of-a-working-gitlab-install)


Edit /etc/gitlab/gitlab.rb
```
external_url 'http://gitlab.kvchmurphy.com'
```

Then
```
gitlab-ctl reconfigure
gitlab-ctl restart
```

Add Remote GIT

```
git remote add gitlab http://gitlab.kvchmurphy.com/hxrsmurf/hxrsmurf-jekyll.git
```