---
layout: post
status: publish
published: true
title: MinIO & Backblaze B2 Integration
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
date: '2021-02-13 12:00:00 -0500'
date_gmt: '2021-02-13 12:00:00 -0500'
categories:
- Articles
tags: []
comments: []
---

MinIO is a great web browser tool to use with Backblaze B2.

Recently, I found the latest MinIO does not support B2 due to eTags. So, a previous version needed to be used.

Here's the info in github.
- https://github.com/minio/minio/issues/11172
- https://github.com/minio/minio/releases/tag/RELEASE.2020-12-16T05-05-17Z

Backblaze's Directions

- https://www.backblaze.com/b2/docs/s3_compatible_api.html
- https://help.backblaze.com/hc/en-us/articles/360047120614-How-to-move-Data-from-an-Existing-Bucket-to-a-new-S3-Compatible-Bucket


```
b2 copy-file-by-id <sourceFileID> <destinationBucketName> <b2FileName>
```

Here's my docker-compose.yaml

```
version: '3'

services:
  minio1:
    image: minio/minio:RELEASE.2020-12-16T05-05-17Z
    ports:
      - "9000:9000"
    environment:
      MINIO_ACCESS_KEY: [B2 Key]
      MINIO_SECRET_KEY: [B2 Secret]
    command: gateway s3 https://s3.us-west-001.backblazeb2.com/
```