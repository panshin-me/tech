---
layout: post
title: Map Grabber
published: true
author: Yura
tags:
    - .NET
    - 'C#'
    - GPS
    - Maps
    - Open Source
    - WinForm
categories:
    - development
    - opensource
    - projects
permalink: /opensource/map-grabber.html
image:
    feature: /assets/posts/2007-04-28-map-grabber/main-screen.jpg
---
Prepare maps for your holidays, your walking, your bike trips, your geocaching&#8230; You can next print them or use them with your GPS!
This utility automatically scrolls, captures, assembles and saves maps (or other window content) from a Web page to a JPG file.
This program is free ware. Developed in C# .NET2.0
<!--more-->
Project source code is licensed under a free software/open source licensing terms:
  
GNU General Public License, version 2.0 or later

### How to use?

  * Go to the desired Web site, maximize your browser window.
  * Locate the desired area on the map and zoom to the desired scale.
  * In order to MapGrabber automatically realize the right scrolling, you have to parameter it according to the Web site.
  * Press the button 1 in MapGrabber (see illustrations), next click on the left/top corner of the map. To avoid capturing the toolbar, you can define the corner just below it.
  * Press the button 2 in MapGrabber, next click on the right/bottom corner of the map.
  * To divide output image by slices, set the steps in one part.
  * If you would like to calibrate maps in time of grabbing, you can use GPS Calibration part of the MapGrabber

You can now Save the settings for future use; each Web site will have its own settings.**
  
![Main Application screen](/assets/posts/2007-04-28-map-grabber/main-screen.jpg)
  
**Menu**
  
`Settings` - Load and save your current settings for future using.
  
`Help` - The link to this page and information about me.

**Map Settings**
  
The position of left/top and right/left bounds of map, without active elements, on the screen. You can set points by enter the coordinates or by clicking on button `Point` and dragging the icon to he's place on the screen.

**Capture Settings**
  
Delay Scroll - When Map grabber moving the map in map display program (Firefox), to program take time to response for her events. So need to delay Map grabber events according to response of display program.
  
Delay Capture - When Map grabber the map in map display program (Firefox), to load new images take some time. So you must set the parameter according to speed image loading.
  
Number of X/Y Steps - How match steps to do.

**Output image settings**
  
Divide Image X/Y - By how match steps divide the output image. Some programs that using output maps on pocket PC, take a lot time to load big image.
  
Map Path - The output image folder.

- With GPS calibration - Enable GPS automatic GPS calibration of output map.

- Show/Hide points - show/hide the map settings and GPS calibration points.

**GPS Calibration**
  
First point X/Y - The point of place that you know her GPS coordinates. You can set points by enter the coordinates or by clicking on button "Point" and dragging the icon to her place on the screen. You can use the magnifier to put the icon exactly to place of GPS coordinates.
  
First point Lat/Lon - The GPS coordinates of point.


![Magnifier Application Window](/assets/posts/2007-04-28-map-grabber/magnifier.jpg)

![Map Sample](/assets/posts
/2007-04-28-map-grabber/capture-screen.jpg)

Prior to start capturing, set the amount of horizontal and vertical steps you desire.
Press the button Start.

### Know Bugs

**found by me and another users.**
  
- Magnifier doesn’t seen to be working
  
- Memory out when grabbing more than 10X10 screens.

### TODO:

**what in next version.**
  
- grab large size maps
  
- The GPSTuner have auto map loading feature. We can use maps with different resolution, and different level of information on map. That provide option in time of zoom out or zoom in, change maps automatically. So I want to add feature - grabbing maps with some levels of zoom.

### Donation

Map Grabber is free software. The author has spent a large amount of time and effort in the development and improvement of it. The continuous development of Map Grabber needs your support. The best way to support and encourage the author, so that this project can be moved forward always, is to donate for Map Grabber project. Click the button below to donate for Map Grabber via PayPal.
<form action="https://www.paypal.com/cgi-bin/webscr" method="post"><input type="hidden" name="phpMyAdmin" value="74cf6475600adbc6783b2928e560cce2"> <input type="hidden" name="cmd" value="_donations"> <input type="hidden" name="business" value="BL3ZJFQ2DN2JC"> <input type="hidden" name="lc" value="GB"> <input type="hidden" name="item_name" value="Map Grabber Application"> <input type="hidden" name="currency_code" value="GBP"> <input type="hidden" name="bn" value="PP-DonationsBF:btn_donateCC_LG.gif:NonHosted"> <input type="image" name="submit" src="https://www.paypal.com/en_US/GB/i/btn/btn_donateCC_LG.gif" alt="PayPal - The safer, easier way to pay online."> <img src="https://www.paypal.com/en_GB/i/scr/pixel.gif" alt="" width="1" height="1" border="0"></form>

### Download

Map Grabber may not be bundled with other software, included on CDs etc, linked to from other web sites or made available for download elsewhere. Link to this page instead.

#### Version 1.2.3 - 12/05/08
  
* [MapGrabber1.2.3Installer.zip](/assets/bin/MapGrabber1.2.3Installer.zip) - Installation
* [MapGrabber1.2.3Binnary.zip](/assets/bin/MapGrabber1.2.3Binnary.zip) - Binnary
* [MapGrabber1.2.3Source.zip](/assets/bin/MapGrabber1.2.3Source.zip) - Source
  
**New Features:**
  - Added output image format choose (JPG, PNG, TIFF).

#### Version 1.2.2 - 26/10/07
  
* [MapGrabber1.2.2Installer.zip](/assets/bin/MapGrabber1.2.2Installer.zip) - Installation
* [MapGrabber1.2.2Binnary.zip](/assets/bin/MapGrabber1.2.2Binnary.zip) - Binnary
* [MapGrabber1.2.2Source.zip](/assets/bin/MapGrabber1.2.2Source.zip) - Source
  
**Resolved bugs:**
  
- resolved bug with GPS collibration.

#### Version 1.2.1 - 25/10/07**
  
* [MapGrabber1.2.1Installer.zip](/assets/bin/MapGrabber1.2.1Binnary.zip) - Installation
* [MapGrabber1.2.1Binnary.zip](/assets/bin/MapGrabber1.2.1Installer.zip) - Binnary
* [MapGrabber1.2.1Source.zip](/assets/bin/MapGrabber1.2.1Source.zip) - Source
  
**New in version:**
  
- changes in user interface.

#### Version 1.2 - 21/09/07
  
* [MapGrabber1.2Installer.zip](/assets/bin/MapGrabber1.2Installer.zip) - Installation
* [MapGrabber1.2Binnary.zip](/assets/bin/MapGrabber1.2Binnary.zip) - Binnary
* [MapGrabber1.2Source.zip](/assets/bin/MapGrabber1.2Source.zip) - Source
  
**New in version:**
  
- status bar in grabbing time.
  
**Resolved bugs:**
  
- resolved some bugs.

#### Version 1.1 - 08/08/07
  
* [MapGrabber1.1Installer.zip](/assets/bin/MapGrabber1.1Installer.zip) - Installation 
* [MapGrabber1.1Binnary.zip](/assets/bin/MapGrabber1.1Binnary.zip) - Binnary
* [MapGrabber1.1Source.zip](/assets/bin/MapGrabber1.1Source.zip) - Source
  
**New in version:**
  
- change map cursor when selecting points for calibration.
- preview the selected points (bounds and calibration).
  
**Resolved bugs:**
  
- This is related to application GPS calibration function. German numbers are separated using the colon symbol like 53,231245 , and application uses the full stop as the separator like 53.231245.
  
- In time of grabbing, pressing on button ESC cause exception.

#### Version 1.0 - 6/28/07
  
* [MapGrabberInstaller.zip](/assets/bin/MapGrabberInstaller.zip) - Installation
* [MapGrabberBinnary.zip](/assets/bin/MapGrabberBinnary.zip) - Binnary
* [MapGrabberSource.zip](/assets/bin/MapGrabberSource.zip) - Source


### Links / Credits


[Project Page on MSDN Code Gallery](http://code.msdn.microsoft.com/MapGrabber)
  
[Project Page on CodePlex](http://www.codeplex.com/MapGrabber)
  
[Project Page on CodeProject](http://www.codeproject.com/KB/cs/MapGrabber.aspx)
  
[GPS Tuner](http://www.gpstuner.com/index.html) - is an off-road navigation software for Pocket PC devices. The maps of Map Grabber is collibrated for this programm.
  
[Capturing the Screen Image in C#](http://www.codeproject.com/csharp/cscapturescreen1.asp)
  
[Processing Global Mouse and Keyboard Hooks in C#](http://www.codeproject.com/csharp/globalhook.asp)

### Disclaimer

Personal use only. Use at your own risk. No technical support given. Don't copy or distribute copyrighted media.
Screen captures will never replace a bought genuine printed map.