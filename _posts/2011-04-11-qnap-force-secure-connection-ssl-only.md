---
layout: post
title: QNAP – Force secure connection (SSL) only
author: Yura
tags:
    - QNAP
    - SSL
categories:
    - misc
    - technology
permalink: /technology/qnap-force-secure-connection-ssl-only.html
image:
    feature: /assets/posts/2011-04-11-qnap-force-secure-connection-ssl-only/qnap-ts-239-pro-ii-plus_1.jpg
---
I played with SSL setting of web - administration of my NAS (QNAP TS-239PROII). And when I switched on force secure connection parameter, I was through up from the site and was not able to open back it.
<!--more--> 
You have two options to remove the parameter to previous value:
  
- First option is just reset your NAS to default settings, but the option will remove all your settings.
  
- And second is more difficult but without loosing all your settings. And the option was suitable for me.

    1. Log into your QNAP device using SSH or Telnet, for instance by using Putty.
    
    2. Open config file in editor: `# vi /mnt/HDA_ROOT/.config/uLinux.conf`
    
    3. Press i button to enter to insert mode
    
    4. Change line: `Force SSL = 1` to `0`
    
    5. Press "esc" to exit from insert mode
    
    6. Press `:wq` to save file

This is it, you can now open web administration by regular way.