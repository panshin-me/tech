---
layout: post
title: VS.Php for Visual Studio Solution Generator
published: true
author: ypanshin
comments: true
date: 2011-04-26 04:04:58
tags:
    - 'C#'
    - php
    - Visual Studio
    - VS
    - VS.Php
categories:
    - development
    - opensource
    - projects
permalink: /opensource/vs-php-for-visual-studio-solution-generator.html
image:
    feature: /assets/posts/2011-04-26-vs-php-for-visual-studio-solution-generator/Explorer-150x150.png
---
For my personal purposes I started to develop themes for Wordpress. I found one VS.Php development tool integrated to visual studio.
<!--more-->
You can download it from here: [http://www.jcxsoftware.com/jcx/](http://www.jcxsoftware.com/jcx/) I like the idea to develop in some environment that I am regular to. But there was one problem: the fast way to create solution from Wordpress directory. As you know, WordPress directory include big amount of files and directories. I did not like the idea to add it one by one. I created console application generated solution and project file for VS.Php tool. The application receive just directory path with files to add to solution. It will create solution file in root and put to processed directory a project file. Using example:

```
VSPhpSolutionGenerator.exe "C:\Wordpress3.2.1\wordpress"
```

It will create the tree:
  
[![](/assets/posts/2011-04-26-vs-php-for-visual-studio-solution-generator/Explorer.png)](#)
  
Download: [VSPhpSolutionGenerator.rar](assets/posts/2011-04-26-vs-php-for-visual-studio-solution-generator/VSPhpSolutionGenerator.rar)