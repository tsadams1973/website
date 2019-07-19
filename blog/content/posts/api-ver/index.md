---
title: "API Versioning in ASP.NET Core"
date: 2019-07-18
draft: false
type: "post"
description: "Using Microsoft aspnet-api-versioning to add API versioning semantics to your ASP.NET Core API"
tags: ["api", "versioning", "swashbuckle", "swagger"]
---

Versioning is an important aspect of API design and implementation. We need to be able change our service and add new features while still providing a stable API our users can consume. I spent a little time with Microsoft's [aspnet-api-versioning](https://github.com/microsoft/aspnet-api-versioning) library, which provides an easy way to add different verioning semantics to your API project.

These libraries are really easy to get started with and there are a handful of useful [samples here](https://github.com/microsoft/aspnet-api-versioning/tree/master/samples).

---

#### Getting Started

Install packages:

```csharp
dotnet add package Swashbuckle.AspNetCore
dotnet add package Microsoft.AspNetCore.Mvc.Versioning --version 3.1.3
dotnet add package Microsoft.Extensions.PlatformAbstractions --version 1.1.0
dotnet add package Microsoft.AspNetCore.Mvc.Versioning.ApiExplorer --version 3.2.0
```

---

You can find my [sample here](https://github.com/tsadams1973/dotnet-core/tree/master/api-ver) if you want a bit of a head start.
