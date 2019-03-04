---
layout: post
title: Kodibuntu + OpenVPN + PIA (privateinternetaccess)
published: true
author: ypanshin
comments: true
date: 2016-04-28 09:04:44
tags:
    - Kodi
    - OpenVPN
    - PIA
    - Xtreamer Ultra 2
categories:
    - technology
permalink: /technology/kodibuntu-openvpn-pia-privateinternetaccess.html
image:
    feature: assets/posts/2016-04-28-kodibuntu-openvpn-pia-privateinternetaccess/800px-Kodi-exit-200x180.png
---
I tried several OS for my cinema room Xtreamer. From beginning I had OpenELEC, this OS has very good performance on Xtreamer. However, OpenELEC does not have browser and for me it is one of deal breaks.
<!--more-->
I installed Windows 10 with Kodi, and performance was not so great. The booting time was long and Flash performance in browser was not enough.

So, I decided to try Android-x86, it worked well, however there was problem with video quality. Sites recognized my Xtreamer as mobile device and reduced video quality.

And, my last try is Kodibuntu. Meanwhile it looks fine, however I would like to use PIA together with Kodi and PIA does not provide client for Kodi. After a research I found a way to set the VPN up.

After Kodibuntu installation, you should "exit" from Kodi. After this you get another login prompt where your username should be inserted automatically. At the right top of the screen, there is a symbol which looks like a sheet with a broken corner. Click on that and select "kodibuntu". After that you enter the password you have given at installation and hit enter.

In desktop mode you can run terminal by hit the keyboard shortcut Ctrl - Alt + T

- Install OpenVPN
```
sudo apt-get install network-manager-openvpn
```
- Get PIA OpenVPN package
```
sudo wget https://www.privateinternetaccess.com/openvpn/openvpn.zip
```
- Unzip
```
unzip openvpn.zip
```
- Test OpenVPN, you can choose any server you like, I used Germany.
```
sudo openvpn --config ./Germany.ovpn
``` 

Use your PIA username and password when it requested.
  
You should get "initialization Sequence Completed" in output. 

TODO: add DNS fixing

Now you can open browser and navigate to https://www.privateinternetaccess.com to see if your connection secured.

- Choose you ovpn file and copy together with certificates to OpenVPN folder. The "ovpn" extension should be changed to "config".
```
sudo cp Germany.ovpn /etc/openvpn/Germany.conf
sudo cp ca.rsa.2048.crt /etc/openvpn/ca.rsa.2048.crt
sudo cp crl.rsa.2048.pem /etc/openvpn/crl.rsa.2048.pem
```      
- You should create PIA credentials to file.
```
sudo vi /etc/openvpn/pia-login.conf
sudo chmod 400 /etc/openvpn/pia-login.conf
```   
- Add to Germany.conf file - point to pia-login.conf
```
sudo vi /etc/openvpn/Germany.conf
```    

Change line: "auth-user-pass" to "auth-user-pass pia-login.conf"

- Change OpenVPN default settings that OpenVPN will start on startup.
```
sudo vi /etc/default/openvpn
```
Add line AUTOSTART="Germany" after #AUTOSTART="home office".
- Do reboot
```
sudo reboot
```

Now you can boot in Kodi and use one of Kodi addons to check your external ip.

- VPN bypass for SSH
```
iptables -t mangle -A PREROUTING -p tcp --dport 22
```
