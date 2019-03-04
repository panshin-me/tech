---
layout: post
title: UI Test with solving Captcha by iMacros
author: Yura
tags:
    - Captcha
    - iMacros
    - UI Test
categories:
    - development
permalink: /development/ui-test-with-solving-captcha-by-imacros.html
---
I found interesting solution for UI testing, it is [iMacros](http://www.iopus.com/iMacros/). But on my site I have captcha when a new user sign in. There is two options to test sign in page is disable captcha for testing time or solve it by some automatic way.
<!--more-->
There is exits services that give you ability soleve captcha automatically by iMacros. But all the services is not for free.
  
I found Captcha Trader the service provide solving captcha by credits that you able to buy or earn by solving other captchas.

To use Captcha Trader you need to register on the site, get API key and earn or buy captcha credits.

To solve the captcha, script get captcha image url from page, and POST it to: http://api.captchatrader.com/submit. Shortly after post the service will automatically return JSON responce with the captcha text.

**Arguments of service**
  
All arguments are required for a successful submission.
  
`api_key`: The API key of the application.
  
`match` (optional): Instead of receiving a text response, receive a boolean response for whether the image is a type of this string.
  
`password`: The password or passkey of the account to submit under in plain text. In some cases it may be preferential to ask the user for their passkey instead of their password. Note that in the future, use of a password may become deprecated to passkey usage.
  
`type`: The type of image this is. See type reference below.
  
`username`: The username of the account to submit under.
  
`value`: The CAPTCHA submission itself, either a string or a file object.

**Types**
  
CaptchaTrader accepts a variety of file image types, but it must be specified. If incorrectly specified, the CAPTCHA will not be solved.
  
`url-jpg`: A url of a jpg file.
  
`url-jpeg`: A url of a jpeg file. Note that this is functionally equivalent to url-jpg.
  
`url-png`: A url of a png file.
  
`url-bmp`: a url of a bmp file.
  
`file`: A multipart/form-data upload of the image.

**Example Response**
  
A typical response will be a JSON encoded string as such:
  
`[1264, "start multipart"]`

Parameters help is from [CaptchaTrader](http://captchatrader.com/) site.

Here is the snapshot macro code to solve the captcha.
```js
// START YOUR CODE

// typically you put this code when you are first able to see the captcha
// the code get url of image from page that captcha on.
var macro = 'CODE:';
macro += "TAG POS=1 TYPE=IMG ATTR=SRC:*/recaptcha/api/* EXTRACT=HREF";
var retcode = iimPlay(macro);
if (retcode == 1) {
   var captchaUrl = iimGetLastExtract();
   var serviceUrl = 'http://api.captchatrader.com/submit';
   var params = 'api_key=';
   params += '&password=';
   params += '&username=';
   params += '&type=';
   params += '&value=' + captchaUrl;

   var xmlhttp;
   if (window.XMLHttpRequest) {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp = new XMLHttpRequest();
   }
   else {// code for IE6, IE5
      xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
   }
   xmlhttp.onreadystatechange = function () {

      if (xmlhttp.readyState == 4 && (xmlhttp.status == 200 ||       xmlhttp.status == )) {
         //Code that will be called when responce will be recived from CaptchaTrader
         onSuccess(xmlhttp.responseText);
      }
   }

   xmlhttp.open("POST", serviceUrl, true);
   xmlhttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
   xmlhttp.setRequestHeader("Content-length", params.length);
   xmlhttp.setRequestHeader("Connection", "close");
   xmlhttp.send(params);
} else {
   errtext = iimGetLastError();
   alert(errtext);
}

function onSuccess(json){
   var res = eval("(" + json + ')');
   var captchaText = res[1];
   captchaText = captchaText.replace(' ', '');

   //this shows an example of how to input the variable into the captcha input
   var macro = "CODE:";
   macro += "TAG POS=1 TYPE=INPUT:TEXT FORM=NAME:someForm ";
   macro += "ATTR=ID:recaptcha_response_field CONTENT=" + captchaText + "\n";
   macro += "TAG POS=1 TYPE=INPUT:IMAGE FORM=ID:someForm "
   macro += "ATTR=ID:SubmitButton";
   var retcode = iimPlay(macro);
   if (retcode < 0) {
      errtext = iimGetLastError();
      alert(errtext);
   } else {
      //Put here code that will be called when captcha will be solved.
   }
}
```
  
