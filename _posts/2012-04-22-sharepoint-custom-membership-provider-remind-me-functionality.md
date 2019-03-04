---
layout: post
title: >
    SharePoint custom membership provider – remind me
    functionality
published: true
author: ypanshin
comments: true
date: 2012-04-22 04:04:56
tags:
    - 'C#'
    - Membership Provider
    - Remember me
    - SharePoint
categories:
    - development
permalink: /development/sharepoint-custom-membership-provider-remind-me-functionality.html
---
My current project is based on SharePoint site, and I manage my users in custom Database. So for the purpose I created custom membership provider and attached to the Sharepoint site. In addition to the changes, I was requested to create a custom login page.
<!--more-->

To login to Sharepoint, after checking password and username, I use the method:
```
...
bool res = SPClaimsUtility.AuthenticateFormsUser(this.Page.Request.Url, userEmal, password);
...
```

However the method does not accept "remember me" flag. I opened the method by reflector and found such lines:
```
...
bool isPersisted = !SPSecurityTokenServiceManager.Local.UseSessionCookies;

... 

SPSessionTokenWriteType local_0 = SPSessionTokenWriteType.WriteSessionCookie;
if (isPersisted)
    local_0 = SPSessionTokenWriteType.WritePersistentCookie;
fam.SetPrincipalAndWriteSessionToken(token, local_0);
...
```
```
SPSessionTokenWriteType.WriteSessionCookie
```

The enum says that these are temporary cookie files, which are erased when you close your browser. When you restart your browser and go back to the site that created the cookie, the website will not recognize you. You will have to log back in (if login is required) or select your preferences/themes again if the site uses these features. A new session cookie will be generated, which will store your browsing information and will be active until you leave the site and close your browser.
```
SPSessionTokenWriteType.WritePersistentCookie
```
The enum says that these cookie files stay in one of your browser's subfolders until you delete them manually or your browser deletes them based on the duration period contained within the persistent cookie's file.

Based on the discover, the solution for "remember me" functionality is:
```
...
SPSecurityTokenServiceManager.Local.UseSessionCookies = !keepMeLoggedIn.Checked;
bool res = SPClaimsUtility.AuthenticateFormsUser(this.Page.Request.Url, userEmal, password);
...
```
The solution add "remind me" functionality to custom log in page.
