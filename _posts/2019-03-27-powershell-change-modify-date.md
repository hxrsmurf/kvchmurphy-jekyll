---
layout: post
status: publish
published: true
title: PowerShell Change Modify Date
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2019-3-27 19:14:00 -0600'
date_gmt: '2019-3-27 19:14:00 -0600'
categories:
- Tutorial
tags: []
comments: []
---

This PowerShell one-liner sets the lastwritetime from null to lastaccesstime. 

	$(Get-Item FILEHERE).lastwritetime = $(Get-Item FILEHERE).lastaccesstime

[Source](https://stackoverflow.com/questions/582553/how-do-i-programmatically-change-the-create-modify-access-date-on-a-file/582638#582638)