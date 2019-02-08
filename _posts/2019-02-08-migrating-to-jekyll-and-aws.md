---
layout: post
status: publish
published: true
title: Migrating to Jekyll and AWS
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2019-02-08 07:58:00 -0600'
date_gmt: '2019-02-08 07:58:00 -0600'
categories:
- Articles
tags: []
comments: []
---

I had this website in a traditional WordPress website (MySQL and debian). I've been learning more about Amazon Web Services products. I have seen a lot of starter blogs/tutorials on doing a static website. I learned a little about Lambda and NodeJS. I found [EnduroJS](https://www.endurojs.com/) which helps create NodeJS websites. However, there was a lot of overhead running NodeJS for my simple website. 

So, I went to [Jekyll](https://jekyllrb.com/) a Ruby based static website generator. And here we are. 

I paired Jekyll with AWS S3, AWS Cloudfront, and Route53. Route53 allows you to point to a Cloudfront distribution point. Then, Cloudfront is used to point to the S3 bucket. Nice! 