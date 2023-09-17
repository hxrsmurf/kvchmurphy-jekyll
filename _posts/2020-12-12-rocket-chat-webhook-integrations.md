---
layout: post
status: publish
published: true
title: Rocket Chat WebHook Integrations
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2020-12-12 12:00:00 -0500'
date_gmt: '2020-12-12 12:00:00 -0500'
categories:
- Articles
tags: []
comments: []
---

I've wanted to trial-and-error an alternative to Discord (self-hosted). I came upon RocketChat.

Some of the integrations I enjoyed playing with are text messaging (SMS) and e-mail. Sort of like a single-app for all my communications.

I currently use Flowroute for SIP via FreePBX (hosted at Cyberlynk). So, I figured I should use them for SMS + RocketChat.

Next up is trying the fancy Twilio (as I've seen that used everywhere).

Once I figured out how to parse the JSON message in RocketChat, all was well. It did take me a few hours to find that Twilio's message is case-sensitive (as of 2020-12-12)!

Here are the integrations on GitHub: https://github.com/hxrsmurf/rocketchat

Another integration was e-mail. Right now I have a custom domain with catch-all on GSuite (now WorkSpaces). I wanted to play with SendGrid + RocketChat.

Turns out RocketChat uses Meteor, which can't parse `multipart/form-data` which SendGrid uses for e-mail!

I might try mailgun or other e-mail gateways later...

Another problem is group texts (MMS). Looks like Twilio handles it...OK, but not the best as it only shows just me, not the whole group members.