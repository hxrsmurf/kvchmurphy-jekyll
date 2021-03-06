---
layout: post
status: publish
published: true
title: How to Expand An LVM Partition
author:
  display_name: kevin
  login: kevin
  email: kevin-wp@hxrsmurf.info
  url: ''
author_login: kevin
author_email: kevin-wp@hxrsmurf.info
wordpress_id: 559
wordpress_url: https://kvchmurphy.com/?p=559
date: '2018-09-23 22:15:01 -0500'
date_gmt: '2018-09-24 02:15:01 -0500'
categories:
- Tutorial
tags: []
comments: []
---
<p>View the physical volume:</p>
<ul>
<li>pvs</li>
</ul>
<p>View the volume group:</p>
<ul>
<li>vgs</li>
</ul>
<p>View the logical volume:</p>
<ul>
<li>lvs</li>
</ul>
<p>Display the logical volumes:</p>
<ul>
<li>lvdisplay</li>
</ul>
<p>Display the volume group details:</p>
<ul>
<li>vgdisplay</li>
</ul>
<p>Extend the actual logical volume:</p>
<ul>
<li>lvextend -l +[Free PE / Size] /dev/[volume group name]/[logical volume]</li>
</ul>
<p>Resize the actual logical volume:</p>
<ul>
<li>resize2fs /dev/[volume group name]/[logical volume]</li>
<li>xfs_growfs /dev/[volume group name]/[logical volume]</li>
</ul>
<p><a href="https://www.tecmint.com/extend-and-reduce-lvms-in-linux/">Tecmint</a> | <a href="https://stackoverflow.com/questions/26305376/resize2fs-bad-magic-number-in-super-block-while-trying-to-open">Stackoverflow</a></p>

===

```
# Unmount the filesystem/partition
umount /dev/sdb1 /mnt/seafile


# Delete the partition
# Create the partition at the same start sector (2048)
# Keep disk signature of Linux, don't overwrite

fdisk /dev/sdb

# Check the filesystem/partition

e2fsck -f /dev/sdb1

# Resize the filesystem/partition

resize2fs /dev/sdb1

# Mount the filesystem/partition

mount /dev/sdb1 /mnt/seafile
```

[Redhat](https://access.redhat.com/articles/1190213)