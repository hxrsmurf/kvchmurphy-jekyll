---
layout: post
status: publish
published: true
title: CloudFormation Template For Simple 3 VPC
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2019-02-15 12:40:00 -0600'
date_gmt: '2019-02-15 12:40:00 -0600'
categories:
- Tutorial
tags: []
comments: []
---

This is a work-in-progress CloudFormation template. The template creates three VPCs. Each VPC has a WAN and NAT subnet. A WAN subnet has an internet gateway while a NAT subnet has a NAT gateway. The route tables for each VPC are updated accordingly. I use this to move between regions for testing purposes. 

[CloudFormation Template]({{site.mediaurl}}/cloudformation/simple-3-vpc.json)
