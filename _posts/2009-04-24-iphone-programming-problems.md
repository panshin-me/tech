---
layout: post
title: iPhone Programming Problems
author: Yura
tags:
    - iPhone
    - JSON
    - Objective C
    - XCode
categories:
    - development
    - technology
permalink: /development/iphone-programming-problems.html
---
In this post I want to collect all problems that I meet in programming for iPhone and solved them.
<!--more-->

  * Application Exception: `[NSCFString JSONValue]: unrecognized selector sent to instance`

I added [JSON framework](http://code.google.com/p/json-framework/) to my iPhone project. And did all things that posted on [installation page](http://code.google.com/p/json-framework/wiki/InstallationInstructions). But when I run my application I received exception when tried to parse JSON string. So I found [solution on the site](http://code.google.com/p/json-framework/issues/detail?id=22). I put '-ObjC -ljson -all\_load' to "Other Linker Flags". And also, "$HOME/Library/SDKs/JSON/$(PLATFORM\_NAME).sdk" to "Additional SDKs"

  * XCode Error: `Error launching remote program: failed to get the task for process XXXX`

When I tried to debug my application on iPhone, I get such error from XCode. The error was after application installation and starting. I found solution [on the site](http://www.iphonedevsdk.com/forum/iphone-sdk-development/28403-error-launching-remote-program-failed-get-task-process-1533-a.html). I just removed code signing entitlements plist file from debug configuration.

  * XCode Error: `syntax error before 'AT_NAME' token«, »error: syntax error before '}' token« and »fatal error: method definition not in @implementation context`

When I compiled code for version 3.0 of iPhone OS I received such error. I found solution [on the site](http://code.google.com/p/json-framework/wiki/InstallationInstructions). I just changed the compiler GCC version to something other than 4.2 and back again to 4.2.