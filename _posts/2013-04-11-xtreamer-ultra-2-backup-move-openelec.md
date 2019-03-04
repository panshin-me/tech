---
layout: post
title: Xtreamer Ultra 2 – Backup / Move OpenELEC
published: true
author: ypanshin
comments: true
date: 2013-04-11 04:04:52
tags:
    - Backup
    - OpenELEC
    - Xtreamer Ultra 2
categories:
    - misc
    - technology
permalink: /technology/xtreamer-ultra-2-backup-move-openelec.html
image:
    feature: /assets/posts/2013-04-11-xtreamer-ultra-2-backup-move-openelec/Xtreamer-Ultra-200x180.jpg
---
Before install a other version of OpenELEC to my Xtreamer, I installed the OS on key stick. When I decided to move the version to Xtreamer internal SSD, I did not want to loose all OpenELEC and XBMC settings.
<!--more-->
Those the steps that I did to backup and restore the settings:

Backup:

1. Enable SSH on OpenELEC, you can do it in OPenELEC settings.
2. Log in to by using one of clients (I used PuTTY [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)). Use the default username "root" and password "openelec".
3. Backup to compressed file two folders by running the commands: 
```
tar -zcvf /storage/xbmc.tar.gz /storage/.xbmc
tar -zcvf /storage/config.tar.gz /storage/.config
```
4. Copy the files to your local computer (I used PSCP utility from same PuTTY download page): 
```
pscp root@192.168.1.48:/storage/xbmc.tar.gz C:\tmp
pscp root@192.168.1.48:/storage/config.tar.gz C:\tmp
```
  
  To process use the default password "openelec". Instead "192.168.1.48" use your OpenELEC  IP, the IP you can get from XMBC system information tab. 
  
5. Remove the files from OpenELEC: 
```
rm -rf /storage/xbmc.tar.gz
rm -rf /storage/config.tar.gz   
```
        
Restore:
        
1. Enable SSH on OpenELEC, you can do it in OPenELEC settings.
2. Log in to by using one of clients (I used PuTTY ). Use the default username "root" and password "openelec".
3. Copy backup files from your local computer (I used PSCP utility from same PuTTY download page) to OpenELEC: 
```
pscp C:\tmp\xbmc.tar.gz root@192.168.1.48:/storage/
pscp C:\tmp\config.tar.gz root@192.168.1.48:/storage/
```
To process use the default password "openelec". Instead "192.168.1.48" use your OpenELEC IP, the IP you can get from XMBC system information tab. 
4. Remove old configuration: 
```
rm -rf /storage/.xbmc
rm -rf /storage/.config
```

5. Before decompress backup files we have to move to root directory: 
```
cd /
```
6. Decompress files: 
```
tar -zxvf /storage/xbmc.tar.gz
tar -zxvf /storage/config.tar.gz
```

7. Remove the files from OpenELEC: 
```
rm -rf /storage/xbmc.tar.gz
rm -rf /storage/config.tar.gz 
```
  
This is it.