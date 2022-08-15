+++ 
date = "2022-07-05T00:00:00Z" 
draft = false 
title = "Resiszing Ubuntu logical volume" 
slug = "resizing-ubuntu-logical-volume" 
+++

Resizing a logical volume on Ubuntu. 

```
sudo lsblk
sudo lvresize -t -v -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
sudo lvresize -v -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
sudo resize2fs -p /dev/mapper/ubuntu--vg-ubuntu--lv
df -h
```
