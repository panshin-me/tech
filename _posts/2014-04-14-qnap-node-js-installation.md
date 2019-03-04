---
layout: post
title: 'QNAP - Node.js installation'
published: true
author: ypanshin
comments: true
date: 2014-04-14 01:04:55
tags:
    - Node.js
    - QNAP
categories:
    - misc
    - technology
permalink: /technology/qnap-node-js-installation.html
image:
    feature: /assets/posts/2014-04-14-qnap-node-js-installation/nodejs-1280x1024-200x180.png
---
The simplest way to install Node.js is by QNAP App center. However the package from app center does not work correctly and in addition, the package installs the outdated version of Node.js.
<!--more-->
  
When I installed Node.js from App Center, I was not able to run npm command, it always returns the error:
```   
module.js:340
    throw err;
          ^
Error: Cannot find module 'npmlog'
    at Function.Module._resolveFilename (module.js:338:15)
    at Function.Module._load (module.js:280:25)
    at Module.require (module.js:362:17)
    at require (module.js:378:17)
    at /share/MD0_DATA/.qpkg/nodejs/node/bin/npm:18:11
    at Object.<anonymous> (/share/MD0_DATA/.qpkg/nodejs/node/bin/npm:86:3)
    at Module._compile (module.js:449:26)
    at Object.Module._extensions..js (module.js:467:10)
    at Module.load (module.js:356:32)
    at Function.Module._load (module.js:312:12)
```     
After several hours of looking on the internet and struggling with installation, I found a way that worked for me:

1. Install the Node.js by QNAP App Center
  
2. Open SSH to your QNAP and login by admin user
	  
For Mac, open terminal and type: ssh {QNAP IP} -l admin
	  
For Windows you can use PuTTY tool from the site: Download page
  
3. Run the commands:
```
cd /share/MD0_DATA/.qpkg/nodejs
wget http://nodejs.org/dist/v0.10.32/node-v0.10.32-linux-x86.tar.gz
tar zxf node-v0.10.32-linux-x86.tar.gz
mv node node-v0.8.22
ln -s node-v0.10.32-linux-x86 node
npm version
```      
Script explanation:
  
Line:2 - download the latest version of Node.js, you can change version "v0.10.32" in the line to any version of Node.js from their site: Node.js
  
Line:3 - uncompress the downloaded file, put attention on version in case you changed it.
  
Line:4 - move old files to tmp directory.
  
Line:5 - create a link with name "node" to the new version of Node.js, you should put attention on the version in name, in case you changed it.
  
Line:6 - the command will display current Node.js version. In my case the output was:


```
{ 
  http_parser: '1.0',
  node: '0.10.32',
  v8: '3.14.5.9',
  ares: '1.9.0-DEV',
  uv: '0.10.28',
  zlib: '1.2.3',
  modules: '11',
  openssl: '1.0.1i',
  npm: '1.4.28' 
}

4. If you try to run any complicated command like "npm install -g grunt-cli" now, you will get an error:
```
Error: setuid user id does not exist
    at /share/MD0_DATA/.qpkg/nodejs/node-v0.10.32-linux-x86/lib/node_modules/npm/node_modules/uid-number/uid-number.js:44:16
    at ChildProcess.exithandler (child_process.js:646:7)
    at ChildProcess.emit (events.js:98:17)
    at maybeClose (child_process.js:756:16)
    at Socket.<anonymous> (child_process.js:969:11)
    at Socket.emit (events.js:95:17)
    at Pipe.close (net.js:465:12)
 ```     
 The problem is QNAP lacks couple of system users available on Linux systems and does not support get or set user-id. So we should modify Node.js source code.
  
Run the command (put attention on the version of Node.js):
```
vi /share/MD0_DATA/.qpkg/nodejs/node-v0.10.32-linux-x86/lib/node_modules/npm/node_modules/uid-number/uid-number.js
```   
The command will open "uid-number.js" file in vi editor. 

You should change line (you can enter to edit mode by pressing "i"):
  
,uidSupport = process.getuid && process.setuid
  
to
  
,uidSupport = false
  
on Line 11 in the file.

Save the file by pressing "Esc" -> "Shift" + ":" -> "w" -> "q"

This is it,
  
Enjoy Node.js latest version.

P.S. As per several comments, different QNAP machines has different paths to ".qpkg" folder. On my machine I have &#8230;./MD0\_DATA/&#8230;, however it can be &#8230;/MDA\_DATA/&#8230;, &#8230;/CACHEDEV1_DATA/&#8230; and so on.

**Updates:**

I tried to install the pm2 package globally like it described in this article: Running NodeJS app on QNAP NAS via pm2. And I had the same issue on my QNAP as the Sergei. I was not able to run this package after installation. I tried Sergei's solution with nodejs installing and it did not work on my TS-239 ProII. So I returned to my steps and at the end, I added the nodejs bin path to PATH with the following command:
```
export PATH=$PATH:/share/MD0_DATA/.qpkg/nodejsv4/node/bin

This command helped me to run pm2 from any location, however, this is a temporary solution, as this path will be lost when you close terminal.
  
We have to add this path every time when NAS was restarted. I decided to use the solution to create autorun.sh as it was described by Sergei with minor changes.

1. Create custom autorun.sh file.
  
We can put all that we need in autorun.sh on the system partition, however, it is better to create your own custom autorun.sh in other location that easily for access.
  
I decided to follow Sergei's steps and created my custom autorun.sh in shared folder:
  
- Create a new shared folder in FileStation (via Web UI), I called for this folder "scripts"
  
- Navigate to this folder from ssh and create autorun.sh file:
```
cd /share/MD0_DATA/scripts
touch autorun.sh
chmod +x autorun.sh
```
- add to autorun.sh file the export commands:
```
vi autorun.sh
```
press 'i' to start file editing and add this content:
```
#!/bin/sh
#set environment variables
SET_ENV_VARS="/share/MD0_DATA/.qpkg/nodejsv4/node/bin"
export PATH=$PATH:$SET_ENV_VARS
echo "export PATH=$PATH" >> /etc/profile
```
Save the file by pressing "Esc" -> "Shift" + ":" -> "w" -> "q"

2. Create autorun.sh in system partition:
  
To create the file on system partition we have to find the name of this partition and mount this partition to have access. Let's find this partition name, we can use the following command:
```
parted $(getcfg system 'System Device') print
```

This command has this output on my machine:
```
Model:  USB DISK MODULE (scsi)
Disk /dev/sdx: 516MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
&nbsp;
Number  Start   End     Size    Type      File system  Flags
 1      16.4kB  2228kB  2212kB  primary   ext2
 2      2228kB  250MB   248MB   primary   ext2
 3      250MB   498MB   248MB   primary   ext2
 4      498MB   516MB   17.4MB  extended
 5      498MB   507MB   8503kB  logical   ext2
 6      507MB   516MB   8897kB  logical   ext2
 ```
 You need the second line (Disk /dev/sdx: 516MB) from this output for the next command:
```
mount -t ext2 /dev/sdx6 /tmp/config
```
Now we have access to this partition, let's create the autorun.sh file and make this file runnuble:
```
cd /tmp/config
touch autorun.sh
chmod +x autorun.sh
```    
Add link to custom autorun.sh to this file:
```
vi autorun.sh
```
press 'i' to start file editing and add this content:
```
#!/bin/sh
/share/MD0_DATA/scripts/autorun.sh
```
Save the file by pressing "Esc" -> "Shift" + ":" -> "w" -> "q"

Unmount the partition:
```
umount /dev/sdx6
```
Now you can restart your QNAP and try to run pm2 from anywhere.