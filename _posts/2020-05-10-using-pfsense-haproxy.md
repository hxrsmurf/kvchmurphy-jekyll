---
layout: post
status: publish
published: true
title: Using pFsense HAProxy
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2020-05-10 12:00:00 -0500'
date_gmt: '2020-05-10 12:00:00 -0500'
categories:
- Tutorial
tags: []
comments: []
---

[Source](https://www.thawes.com/2018/01/configuring-pfsense-haproxy-http-https/)

In pFsense, open HAProxy:

![image](https://cdn.kvchmurphy.com/content/images/2020/05/image.png)

1. Select the "Backend" tab
2. Select "Add"
3. Input data in the "Name" field, select the "+" to add a backend server
4. Input a server address and port
5. Select "Basic" for the "Health check method" (for using Ghost blog)

![image](https://cdn.kvchmurphy.com/content/images/2020/05/image-2.png)

6. Select the "Frontend" tab
7. Input data in the "Name" and "Description" field
8. Input an IP in the "Custom address" (I have a virtual IP in pFsense)
9. Select "http / https(offloading)" in "Type"

![image](https://cdn.kvchmurphy.com/content/images/2020/05/image-3.png)

10. Scroll down and add an entry to "Access Control Lists"
11. For example, the ACL name is "kvch" and IF the host starts with "kvchmurphy.com"
12. Scroll down and add an entry to the "Actions"
13. For example, use the backend "ghost-kvch" if the ACL is "kvch"

![image](https://cdn.kvchmurphy.com/content/images/2020/05/image-4.png)

14. For HTTP to HTTPS redirection, select "http-request redirect" under action and input the below

```
code 301 location https://%[hdr(host)]%[path]
```

![image](https://cdn.kvchmurphy.com/content/images/2020/05/image-5.png)