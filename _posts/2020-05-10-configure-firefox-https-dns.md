---
layout: post
status: publish
published: true
title: Configure Firefox DNS-over-HTTPS
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2020-05-10 11:00:00 -0500'
date_gmt: '2020-05-10 11:00:00 -0500'
categories:
- Tutorial
tags: []
comments: []
---

[Source](https://support.mozilla.org/en-US/kb/firefox-dns-over-https#w_excluding-specific-domains)

I had to do this because I have publicly routable domains in my homelab.

You can configure exceptions so that Firefox uses your OS resolver instead of DOH:

1. Type about:config in the address bar and press Enter.
2. A warning page may appear. Click `Accept the Risk and Continue` to continue to the about:config page.
3. Search for `network.trr.excluded-domains`.
4. Click the Edit button next to the preference.
5. Add domains, separated by commas, to the list and click on the checkmark to save the change.

Note: Do not remove any domains from the list.