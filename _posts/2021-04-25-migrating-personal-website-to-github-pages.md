---
layout: post
status: publish
published: true
title: Migrating Personal Website to Jekyll + GitHub Pages
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2021-04-25 12:00:00 -0500'
date_gmt: '2021-04-25 12:00:00 -0500'
categories:
- Articles
tags: []
comments: []
---

Over this last Saturday and Sunday, I finally sat down and migrated my old, static HTML website to Jekyll format. Jekyll is a static website generator based in Ruby.

hxrsmurf.github.io/hxrsmurf.info

I opted to do Data Files instead of Collections. I may regret this later. Data Files require some additional files/folders (_includes and _data). The way I laid out the website (sure it's not the best) caused some pain creating all these files/folders. So, I opted to create a short PowerShell script to dynamically stage these! Of course I only thought to do this when I was almost done!

The old website was using a free CSS template I had downloaded 10+ years ago! This was the first time I had gone into a CSS template to modify it. I had always just downloaded and uploaded the CSS templates I liked. It was cool to see how similar CSS templates are to something I'm more familiar with like PowerShell and Python.

Part of the CSS learning was position: fixed. I wanted to have one of those up-arrows that followed you around on the website. I found some articles online and got it working. To figure out the dimensions of the arrow, I took a screenshot of the area I was thinking of putting the arrow. Then, I used GIMP to draw the basic arrow. Within CSS I added the appropriate configuration and voila! Hopefully, the arrow isn't too intrusive.

For the social media icons, I borrowed them all from the respective Twitter Profiles. Might as well stay as "official" as I can! Some of the icons were circles and some were squares. I liked the circle look, so I opted to throw them in GIMP and make circles out of them.

Within GitHub, I created a [Repo Project](https://github.com/hxrsmurf/hxrsmurf-jekyll/projects/1) to keep track of the random ideas I had. The Project also has the option for some automation, like new Pull Requests go to To do and completed Pull Requests go to Done.

While I am more familiar with hosting static HTML with nginx/Apache, I opted to use GitHub Pages with their [Jekyll Automatic Deployment](https://jekyllrb.com/docs/continuous-integration/github-actions/). I've been learning about CI/CD via Azure DevOps and GitLab, so this wasn't too unfamiliar to me.

Overall, this was really fun to just figure out. I'm glad to have finally sat down and converted to something slightly more sustainable and easier to update...and automatic! The YAML was easy for me as I did a lot of that at AWS with CloudFormation. Navigating Jekyll was not too bad, too since I had delved into that before, so I knew the general layout.