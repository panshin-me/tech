---
layout: post
title: >
    Sending email by Google SMTP server using Nodemailer 2.x
    with handlebarsjs as tempates engine
published: true
author: ypanshin
comments: true
date: 2016-04-25 05:04:47
tags:
    - domain alias
    - express
    - G Suite
    - google
    - handlebarsjs
    - Node.js
    - Nodemailer 2.x
    - smtp
categories:
    - development
permalink: /development/sending-email-by-google-smtp-server-using-nodemailer-2-x-with-handlebarsjs-as-tempates-engine.html
image:
    feature: /assets/posts/2016-04-25-sending-email-by-google-smtp-server-using-nodemailer-2-x-with-handlebarsjs-as-tempates-engine/nodejs-1280x1024-200x180.png
---
For my latest project I got a domain, let call it as "appdomain.com". From this domain I would like to send emails from my application. However, I don't like idea to set up my SMTP server, so I prefer to use gmail instead. I have an G Suite subscription from days when Google gave this subscription for free :), however this subscription does not allow to add primary domain anymore. I added the new domain as alias to my primary domain, let's call it as "primarydomain.com".
<!--more-->
The issue with domain alias that there is no way to use this alias as username to login to gmail SMTP server. And when some external application try to send thought gmail SMTP server, the server replace from field with logged in username. So in my case if I try to send email with logged in user: noreply@primarydomain.com and from field: noreply@appdomain.com (alias for noreply@primarydomain.com), gmail SMTP server will put noreply@primarydomain.com to from field. And end user will receive email from noreply@primarydomain.com.

To fix this issue you should make those steps:

  1. Login to gmail.com with noreply@primarydomain.com user.
  2. Click the gear icon in the upper right corner.
  3. Click "Settings".
  4. Select "Accounts" tab.
  5. In section "Send mail as:" click on "Add another email address" link.
  6. In the popup window enter name and alias email "noreply@appdomain.com".
  7. Uncheck "Treat as an alias." checkbox.
  8. Click on "Next Step" button.
  9. This popup window will be closed.
 10. Click on "edit info" next to new added row with noreply@appdomain.com email.
 11. In the popup window click on "Next step".
 12. Select "Send through appdomain.com SMTP servers"
 13. Fill in form gmail SMTP details: 
      * SMTP Server: smtp.gmail.com
      * Username: noreply@primarydomain.com (primary username)
      * Password: (primary account password)
      * Select "Secured connection using TSL"
      * Port: 587
 14. Click on "Save Changes" button

You can validate your settings by sending a new email from noreply@appdomain.com (you should have dropdown list in From field in gmail UI).

To allow authentication to SMTP server from Nodemailer, we should change "noreply" account security settings.

  1. In gmail UI click on round icon with name in upper right corner.
  2. Click on "My account" button.
  3. In "Sign-in & security" section, click on "Connected apps & sites" link
  4. At the bottom of this section, switch on "Allow less secure apps:".

Ok, we finished with gmail configurations.

I developed this project by using nodejs environment and express as server. After spending some time to find a best email sending module I choose Nodemailer 2 with handlebarjs as templates engine.

First of all let's Install pre-requirements:
  
[Nodemailer 2](https://nodemailer.com/)
```
npm install nodemailer --save
```

[node-email-templates](https://github.com/crocodilejs/node-email-templates)
```
npm install email-templates --save
```

handlebars
```
npm install handlebars --save
``` 


For each of your email templates create a folder. In my example I created a folder for activation email. In this folder you should create three files

  1. html.{ext} (required) - html format for this email, with extension according to template engine. In my case I use handlebars, so I use "html.hbs".
  2. style.css (optional) - styles file for html format
  3. text.{ext} (optional) - text format content for this email.

At the end you will have such tree:
```
templates/
—activation-email/
——html.hbs
——style.css
——text.hbs
```
Next step, let's create wrapper for Nodemailer functionality:
```javascript
function mailer() {
  var defaults = { from: 'noreply@appdomain.com' };
  var smtpSettings = {
    host: 'smtp.gmail.com',
    port: 465,
    secure: true, // use SSL
    auth: {
      user: 'noreply@primarydomain.com',
      pass: 'primary user password'
    }
  };
  var transporter = nodemailer.createTransport(smtpSettings;
  var templatesDir = path.join(__dirname, '/templates');// template folder path
  var activationSend = transporter.templateSender(new EmailTemplate(path.join(templatesDir, 'activation-email')), defaults);

  /**
   * Activation email context
   * @typedef ActivationEmailContext
   * @property [year] {Number} - current year for copyright footer
   * @property name {String} - recipient name
   * @property activation_url {String} - account activation url
   */

  /**
   * Send activation email
   * @param email {String} - recipient email
   * @param context {ActivationEmailContext} - activation email context
   * @returns {Promise}
   */
  this.activation = function(email, context){
    context.year = context.year || new Date().getFullYear();
    return activationSend({ to: email, subject: 'Activate your account' }, context);
  }
}
```

I don't think that the code above need additional explanation.