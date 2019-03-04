---
layout: post
title: Picasa2WordPress Improvement
author: Yura
tags:
    - Photos
    - php
    - Picasa
    - Picasa Button API
    - Picasa2Wordpress
categories:
    - development
    - opensource
    - projects
permalink: /opensource/picasa2wordpress-improvement.html
---
I organize my personal photo library by Picasa from Google. And I would like to post full albums with photos with a little amount of buttons presses to my WordPress based blog, but I didn't find something suitable for me from huge count of plugins for WordPress.
<!--more--> Whatever I found a script "[Picasa2Wordpress](http://clyang.net/blog/2009/02/06/128)" that use [Picasa Button API](http://code.google.com/apis/picasa/docs/button_api.html) and it's what I really need. But it wasn't enough for me. I was need to post post in additional to upload photos, so I Improve the script.

### Features:
  1. Upload Photos to WordPress blog by Picasa application.
  2. Provide ability to add uploaded photos to exist post/page.
  3. Post new post with photos.

### Installation Instructions:

- Download
    * Version: 1.1: [Picasa2Wordpress1.1.zip](assets/bin/Picasa2Wordpress1.1.zip)
    
    Fix: I found bug in post's DropDown that showed limited list.

    * Version: 1.0: [Picasa2Wordpress.zip](assets/bin/Picasa2Wordpress.zip)

- Unzip it, and put extracted files (should be 5 files) under your WordPress wp-admin directory.
- Optionally you can change some setting in a file picasa_post.php. 
    * $postCategory - the categories that new post will be added to.
    * $postStatus - the status of new post (draft,publish,pending).
    * $postParent - the parent post id for new post.
    * $galleryTag - the gallery tag that will be automatically added to end of new post.
- Go to [Picasa Button Generator](http://clyang.net/blog/picasa2wordpress/) to get your own Picasa button (picasa2wordpress.pbz). This generator can let you define the tooltip in your own language.
- Put picasa2wordpress.pbz at the root directory of your WordPress.
- Type picasa://importbutton/?url=http://your.blogs.url/picasa2wordpress.pbz at browser’s navigation bar. Picasa will be launched and install the button automatically.
- After you confirm to install the WordPress button in Picasa, you may add it to your Picasa panel.