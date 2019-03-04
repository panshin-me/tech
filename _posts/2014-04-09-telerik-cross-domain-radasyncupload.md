---
layout: post
title: Telerik Cross domain RadAsyncUpload
published: true
author: ypanshin
comments: true
date: 2014-04-09 10:04:28
tags:
    - .NET
    - IE
    - Javascript
    - Telerik
categories:
    - development
permalink: /development/telerik-cross-domain-radasyncupload.html
image:
    feature: /assets/posts/2014-04-09-telerik-cross-domain-radasyncupload/Telerik_Logo-200x180.jpeg
---
My last project was linked to Telerik RadAsyncUpload control. The requirements was to upload the files to separate server than the control exists on.
<!--more-->

I found an example from Telerik guy: Hristo Valyavicharski that explained how to solve cross domain problem that exists when the control try to upload files to other server.
  
[http://www.telerik.com/forums/cross-domain-radupload](http://www.telerik.com/forums/cross-domain-radupload)

He suggest to create two sites Web1 and Web2. The Web1 will serve custom overridden AsyncUploadHandler to save files to. And the Web2 will serve the main page form with the control on it.
  
The Web1 should be configured in web.config to accept cross domain requests:
```
<system.webServer>
	<httpProtocol>
	  <customHeaders>
		<add name="Access-Control-Allow-Origin" value="*" />
		<add name="Access-Control-Allow-Headers" value="Origin,cache-control,content-type,man,messagetype" />
	  </customHeaders>
	</httpProtocol> 
</system.webServer>
```     

And there is another important configuration that the temporary folder should exists an be same on both servers.
```
<telerik:RadAsyncUpload
    ID="RadAsyncUpload1"
    DisablePlugins="true"
    TemporaryFolder="C:\\Temp\"
    EnablePermissionsCheck="false"
    runat="server">
</telerik:RadAsyncUpload>
```      
 
The solution that Hristo suggested works fine in Chrome, Firefox however it throw "Access Denied" exception in IE. The problem is when Telerik control make upload in iFrame it try to access to the results of the upload.
  
The results exists in iFrame document that loaded from other domain. IE does not give access to {iFrame}.contentDocument or {iFrame}.contentWindow.document objects.
  
I found some work around the problem:
  
1. The relation between main site and files service should be like this: both sites should have same root domain:
	  
Main site domain: sample.com - Files service domain: files.sample.com
	  
Main site domain: main.sample.com - Files service domain: files.sample.com
	  
Main site domain: main.sample.com - Files service domain: sample.com
  
2. We should set document.domain object on both documents: on main page and iFrame to "sample.com". It does not matter if the object already hold the value, just set it.
	  
And here is the catch, the catch is that we don't have strait way to insert the script to iFrame, that the script will run when iFrame will be loaded.
  
I did some work around to add the script to iFrame content:
  
By the Telerik solution we have Web1 with custom handler that accept uploaded files. So we should override ProcessRequest method to add the script to all outputs of the handler.
```
static string BROWSER = "IE";
static string VERSION = 10;
public new void ProcessRequest(HttpContext context)
{
	var documentDomain = "sample.com";
	//Check if the browser is IE and the version is less that 10.
	if (context.Request.Browser.Type.ToUpper().Contains(BROWSER))
	{
		if (context.Request.Browser.MajorVersion < VERSION)
		{
			//Attach script fix to result
			context.Response.Write(String.Format("<script type=\"text/javascript\">document.domain = \"{0}\";</script>", documentDomain));
		}
	}
	base.ProcessRequest(context);
}
```

Do not forget to add "" to main document.

The script injection is required just for IE 10 enough to add script to main document.

I hope is will save you several days of struggling. 

Have a happy coding.

P.S. By the way, Hristo did not mention in his solution that they have an problem in their handler with IsReusable property.
  
Null Exception With Overridden AsyncUploadHandler - http://www.telerik.com/forums/null-exception-with-overridden-asyncuploadhandler
  
To solve the problem add the lines to your handler:
```
bool IHttpHandler.IsReusable
{
	get
	{
		return false;
	}
}
```
  
