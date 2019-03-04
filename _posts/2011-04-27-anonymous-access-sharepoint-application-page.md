---
layout: post
title: Anonymous Access SharePoint Application Page
author: Yura
tags:
    - 'C#'
    - SharePoint
categories:
    - development
---
Generally when creating a page in SharePoint it inheritance from LayoutsPageBase, however a public page has to inheritance from UnsecuredLayoutsPageBase and overriding AllowAnonymousAccess property.
<!--more-->
```
public partial class ForgotPassword: UnsecuredLayoutsPageBase
{
    protected override boolAllowAnonymousAccess { get{ return true; } }

    protected void Page_Load(objectsender, EventArgs e)
    {
    }
}
```