---
layout: post
title: 'Converter Ip->Number / Number->Ip'
author: Yura
tags:
    - Converter
    - Formula
    - Ip
    - Ip Number
categories:
    - misc
    - projects
permalink: /projects/converter-ip-number.html
---
<link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
<link href="https://unpkg.com/@angular/material/prebuilt-themes/indigo-pink.css" rel="stylesheet">

Free tool translate IP address from dotted-decimal address to decimal format and vice-versa.
<!--more-->
<ip-number class="reset"></ip-number>


## Convert Ip to Ip Number
```
Ip = AAA.BBB.CCC.DDD
Number = 256^3 * AAA + 256^2 * BBB + 256^1 * CCC + 256^0 * DDD
```

## Convert Ip Number to Ip
```
Ip -> AAA.BBB.CCC.DDD

// Floor – returns the value of a number rounded DOWNWARDS to the nearest integer.
DDD = Number % 256
CCC = Floor(Number / 256) % 256
BBB = Floor(Number / 256^2) % 256
AAA = Floor(Number / 256^3) % 256
```

<script src="/assets/js/ps-elements.js"></script>