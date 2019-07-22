---
title: "API Versioning in ASP.NET Core"
date: 2019-07-21
draft: false
type: "post"
description: "Using Microsoft aspnet-api-versioning to add API versioning semantics to your ASP.NET Core API"
tags: ["api", "versioning", "swashbuckle", "swagger"]
---

Versioning is an important aspect of API design and implementation. We want to be able change our service and add new features while still providing a stable API that our users can consume. To that end I recently spent a little time with Microsoft's [aspnet-api-versioning](https://github.com/microsoft/aspnet-api-versioning) library to learn how it provides an easy way to add different verioning semantics to your API project.

These libraries are really easy to get started with and there are a handful of useful [samples here](https://github.com/microsoft/aspnet-api-versioning/tree/master/samples).

---

#### Getting Started

First thing we will need is a new ASP.NET Core Web API project. We will create one with the CLI. Open your favorite terminal and run the following commands:

```csharp
mkdir api-ver
cd api-ver
dotnet new webapi
```

These will create a new API project named api-ver in the current directory. To open it with Visaul Studio Code, simply type `code .`.

You should be here:
{{< imgproc api-ver-1 Resize "800x" "VS Code" "Figure 1" />}}

To get our dependencies out of the way upfront, go ahead and the following packages to your project. My practice is to add packages via the CLI from the terminal in VS Code, like this:

```csharp
dotnet add package Swashbuckle.AspNetCore
dotnet add package Microsoft.AspNetCore.Mvc.Versioning --version 3.1.3
dotnet add package Microsoft.Extensions.PlatformAbstractions --version 1.1.0
dotnet add package Microsoft.AspNetCore.Mvc.Versioning.ApiExplorer --version 3.2.0
```

---

#### Adding Swagger to your API

Swashbuckle provides swagger tooling for ASP.NET Core APIs. We will be using the Swagger UI for this post, so let's add that to our API project before we do anything else.

First we need to register the Swagger generator service. In the ConfigureServices method of our StartUp.cs file add the following:

```csharp
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new Info { Title = "Test API Versioning", Version = "v1" });
});
```

You will need to add a `using Swashbuckle.AspNetCore.Swagger;` to make this work.

*Note:* SwaggerGen is the service that will generate Swagger documents directly from our endpoints.

Ofcourse, we also have to add the middleware to expose the Swagger endoints to our StartUp.cs. While we're at it we will also add the middleware to expose the API documentation. To do all of this we will add these lines to the Configure method of our Startup.cs file *after* `app.UseMvc()`:

```csharp
app.UseSwagger();

app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "My Test API V1");
});
```

Now, if we run our project (`dotnet run` from the VS Code terminal), we will be able to see our Swagger UI at "*application-url/swagger*". If you haven't made any other changes to your project that will likely be `https://localhost:5001/swagger`. You should see something like this:

{{< imgproc api-ver-2 Resize "800x" "swagger" "Figure 2" />}}

---

#### Wasn't this supposed to be about versioning?

Right. Back to the versioning.

---

You can find my [sample here](https://github.com/tsadams1973/dotnet-core/tree/master/api-ver) if you want a bit of a head start.
