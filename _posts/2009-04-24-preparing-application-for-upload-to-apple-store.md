---
layout: post
title: Preparing application for upload to Apple store
author: Yura
tags:
    - Apple Store
    - Configuration
    - Distribution
    - iPhone
    - Objective C
categories:
    - development
    - misc
    - technology
permalink:
    /development/preparing-application-for-upload-to-apple-store.html
---
After all steps that you did with your project of developing new amazing application for iPhone, you will come to last step - deployment. The step is not so easyest as it look like. <!--more--> I want to provide in this post the steps that I did to publish my application.Step 1:
<!--more-->
Prepare all information that you will need to post in apple store about your application:

  1. Application name
  2. Application description
  3. Primary and secondary categories
  4. SKU number - a unique numerical identifier for your application.
  5. Keywords
  6. Application URL
  7. Support URL
  8. Support email address
  9. Some demo account with full acess - the details of any test accounts that Apple store reviwers will use for testing your application. This can include usernames, passwords, access codes, etc.
 10. Application rating details - the rating is base on content of your application, if your application contain any obscene, pornographic, offensive or defamatory content or materials of any kind (text, graphics, images, photographs, etc.), or other content or materials that in Apple’s reasonable judgment may be found objectionable.
 11. You need prepair Large icon 512X512 pixels. When I prepaired this image it was png format with shadow, but when I uploaded it, it didn't look god, so I changed it to jpg with white background and without transparent areas.
 12. Also you need one or up to five screens shots.
 13. Choose your application price tier - Apple will take from you 30% from the price. If you will choose price tier 4, your application in US will cost $3.99 but you will get just $2.80.
 14. You can prepair Name, Description  for other languages.

For now you have all information , for start with Apple store, exept a application itelf.

For preparing to upload binary file of your application you need  finish follow steps:

  1. You need to get iPhone Distribution Certificate. You can read about it on iPhone Developer Programm in distribution section.
  2. Prepare build configuration for Distribution.
  3. Check target build configuration, you must set it to: 
      * Base SDK - your minimum OS Version, the version you will need to put info.plist.
      * Code Signing Identity->Any iPhone OS Device  - you need to choose your distribution certificate.
      * Code Signing Resouce Rules Path - $(SDKROOT)/ResourceRules.plist
  4. Check your Info.plist: 
      * MinimumOSVersion - set this version like you set in build configuration.
      * Bundle identifier - it must be like you fill in developer portal. com.YourCompanyName.${PRODUCT_NAME:identifier}
  5. Choose active compilation type to Device - Version. It's important! You must compile for device and not for emulator.
  6. Go to binnary file folde, compress file and upload to Apple store.

Ok, if all pass without exeption, you will have time to relax till Apple finish review your application.

Some exeptions that I get when uploaded application to Apple store:

  * When you upload your application by "Upload application" screen in iTuness Connect portal and get such error:
  
     `"The binary you uploaded was invalid. The signature was invalid, or it was not signed with an Apple submission certificate"`
  
    You can use Application Loader application from Apple. The application provide you more explaining about errors in your binary file. The application you can get from iTunes connect portal, in "Manage your applications" section. [Link](http://itunesconnect.apple.com/apploader/ApplicationLoader_1.2.dmg)
  * If you get such exeption:
  
    `YourAppName.app/icon.png: icon is not in the proper device format Info.plist does not contain a CFBundleResourceSpecification Application failed codesign verification`
  
    Sometimes it does not mean that your icon is wrong, and even it is not lack of CFBundleResourceSpecification in Info.plist.
  
    It can be that you compiled your application not for device and for simulator.
  
    P.S. CFBundleResourceSpecification key is like "Code Signing Resouce Rules Path" in target configuration. If you put it in target configuration you don't need it in Info.plist.

Good Luck