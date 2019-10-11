---
title: "Using custom middleware to handle MsalUiRequired exceptions."
date: 2019-08-05T20:17:00-04:00
draft: true
type: "post"
description: "If you are unable to use filters to handle exceptions when requesting access tokens this middleware solution might help.l"
tags: ["azure", "b2c", "msal", "core"]
---

If you are using Microsoft Azure AD or Azure AD B2C as part of your IAM solution, odds are you are also using the Microsoft Authentication Library, [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/wiki), to help you manage your tokens. This convenient library helps you acquire tokens that you can use to access APIs protected by Azure AD. It is useful and will save you a lot of time, but is not without its limitations.
