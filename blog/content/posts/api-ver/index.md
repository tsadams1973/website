---
title: "API Versioning in ASP.NET Core"
date: 2019-07-21
draft: false
type: "post"
description: "Using Microsoft aspnet-api-versioning to add API versioning semantics to your ASP.NET Core API"
tags: ["api", "versioning", "swashbuckle", "swagger"]
---

Versioning is an important aspect of API design and implementation. We want to be able change our service and add new features while still providing a stable API that our users can consume. To that end I recently spent a little time with Microsoft's [aspnet-api-versioning](https://github.com/microsoft/aspnet-api-versioning) library to learn how it provides an easy way to add different versioning semantics to your API project.

These libraries are really easy to get started with and there are a handful of useful [samples here](https://github.com/microsoft/aspnet-api-versioning/tree/master/samples).

---

#### Getting Started

First thing we will need is a new ASP.NET Core Web API project. We will create one with the CLI. Open your favorite terminal and run the following commands:

```csharp
mkdir api-ver
cd api-ver
dotnet new webapi
```

These will create a new API project named api-ver in the current directory. To open it with Visual Studio Code, simply type `code .`.

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

Of course, we also have to add the middleware to expose the Swagger endpoints to our StartUp.cs. While we're at it we will also add the middleware to expose the API documentation. To do all of this we will add these lines to the Configure method of our Startup.cs file *after* `app.UseMvc()`:

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

Right. Back to the versioning. Our current API lacks a coherent versioning strategy, so let's fix that. Fortunately, we already added the needed dependencies earlier, so to start, we will add a new versioning service to our ConfigureServices method in our StartUp.cs class.

Add the following after `services.AddMvc()`:

```csharp
 services.AddApiVersioning();
```

Now, navigate to our "ValuesController". We will add URL based versioning, so first we will replace the default route:

```csharp
[Route("api/[controller]")]
```

With the new route:

```csharp
[Route("api/v{version:apiVersion}/[controller]")]
```

And since we want to declare a version for our API, we also need to add the following attribute above that route on our controller:

```csharp
[ApiVersion("1.0")]
```

Now we should have a new, versioned resource in our API. Go to the terminal, type `dotnet run` and launch your broser of choice. Navigate to your swagger endpoint (`https://localhost:5001/swagger`) and let's see.

You will see something like this:
{{< imgproc api-ver-3 Resize "800x" "swagger" "Figure 3" />}}

You will notice that the endpoints look wrong: `/api/v{version}/Values` doesn't seem right. But if we navigate to our "GET" endpoint and choose "Try it out", we will notice we are given a textbox to choose our verion. If we enter a "1" in that box and click "Execute", we will see that our API runs successfully at the expected `https://localhost:5001/api/v1/Values` endpoint:

{{< imgproc api-ver-4 Resize "800x" "swagger" "Figure 4" />}}

If you want to confirm that it doesn't work for any other versions, please feel free to experiment with that.

So, while it seems our versioning is working, clearly our swagger is not.

---

#### Fixing up Swagger

To get our SwaggerUI to accurately reflect the state of our API, we will borrow heavily from this [sample](https://github.com/microsoft/aspnet-api-versioning/tree/master/samples/aspnetcore/SwaggerSample).

First we add two helper classes to our project:

* *ConfigureSwaggerOptions.cs*

* *SwaggerDefaultValues.cs*

**ConfigureSwaggerOptions.cs**
```csharp

using Microsoft.AspNetCore.Mvc.ApiExplorer;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Options;
using Swashbuckle.AspNetCore.Swagger;
using Swashbuckle.AspNetCore.SwaggerGen;

namespace api_ver
{
    /// <summary>
    /// Configures the Swagger generation options.
    /// </summary>
    /// <remarks>This allows API versioning to define a Swagger document per API version after the
    /// <see cref="IApiVersionDescriptionProvider"/> service has been resolved from the service container.</remarks>
    public class ConfigureSwaggerOptions : IConfigureOptions<SwaggerGenOptions>
    {
        readonly IApiVersionDescriptionProvider provider;

        /// <summary>
        /// Initializes a new instance of the <see cref="ConfigureSwaggerOptions"/> class.
        /// </summary>
        /// <param name="provider">The <see cref="IApiVersionDescriptionProvider">provider</see> used to generate Swagger documents.</param>
        public ConfigureSwaggerOptions( IApiVersionDescriptionProvider provider ) => this.provider = provider;

        /// <inheritdoc />
        public void Configure( SwaggerGenOptions options )
        {
            // add a swagger document for each discovered API version
            // note: you might choose to skip or document deprecated API versions differently
            foreach ( var description in provider.ApiVersionDescriptions )
            {
                options.SwaggerDoc( description.GroupName, CreateInfoForApiVersion( description ) );
            }
        }

        static Info CreateInfoForApiVersion( ApiVersionDescription description )
        {
            var info = new Info()
            {
                Title = "Test API Versioning",
                Version = description.ApiVersion.ToString(),
            };

            if ( description.IsDeprecated )
            {
                info.Description += " This API version has been deprecated.";
            }

            return info;
        }
    }
}
```

**SwaggerDefaultValues.cs**
```csharp

using Microsoft.AspNetCore.Mvc.ApiExplorer;
using Swashbuckle.AspNetCore.Swagger;
using Swashbuckle.AspNetCore.SwaggerGen;
using System.Linq;

namespace api_ver
{
    /// <summary>
    /// Represents the Swagger/Swashbuckle operation filter used to document the implicit API version parameter.
    /// </summary>
    /// <remarks>This <see cref="IOperationFilter"/> is only required due to bugs in the <see cref="SwaggerGenerator"/>.
    /// Once they are fixed and published, this class can be removed.</remarks>
    public class SwaggerDefaultValues : IOperationFilter
    {
        /// <summary>
        /// Applies the filter to the specified operation using the given context.
        /// </summary>
        /// <param name="operation">The operation to apply the filter to.</param>
        /// <param name="context">The current operation filter context.</param>
        public void Apply( Operation operation, OperationFilterContext context )
        {
            var apiDescription = context.ApiDescription;

            operation.Deprecated |= apiDescription.IsDeprecated();

            if ( operation.Parameters == null )
            {
                return;
            }

            // REF: https://github.com/domaindrivendev/Swashbuckle.AspNetCore/issues/412
            // REF: https://github.com/domaindrivendev/Swashbuckle.AspNetCore/pull/413
            foreach ( var parameter in operation.Parameters.OfType<NonBodyParameter>() )
            {
                var description = apiDescription.ParameterDescriptions.First( p => p.Name == parameter.Name );

                if ( parameter.Description == null )
                {
                    parameter.Description = description.ModelMetadata?.Description;
                }

                if ( parameter.Default == null )
                {
                    parameter.Default = description.DefaultValue;
                }

                parameter.Required |= description.IsRequired;
            }
        }
    }
}
```

With those in place we will navigate back to our "StartUp.cs" file and make a few changes. First, add the `AddVersionedApi` service after the `AddVersioning` service like so:

```csharp
services.AddVersionedApiExplorer(options =>
{
    options.GroupNameFormat = "'v'VVV";
    options.SubstituteApiVersionInUrl = true;
});
```

Next add the `AddTransient` service to the "StartUp.cs" class after `AddVersionedApiExplorere`:

```csharp
services.AddTransient<IConfigureOptions<SwaggerGenOptions>, ConfigureSwaggerOptions>();
```

*Note:* You might need to add: `using Swashbuckle.AspNetCore.SwaggerGen;`.

Finally (at least as far as services go), we will want to update our `AddSwaggerGen` from:

```csharp
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new Info { Title = "Test API Versioning", Version = "v1" });
});
```

To:

```csharp
services.AddSwaggerGen(c =>
{
    c.OperationFilter<SwaggerDefaultValues>();
});

```

With the changes to our services in place, the last update we need to make is to the SwaggerUI middleware in the "Configure" method of the "StartUp.cs" class. First we will need to add the parameter `IApiVersionDescriptionProvider provider` to the signature of the "Configure" method so that is looks like this:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, IApiVersionDescriptionProvider provider)
```

*Note:* We will also need to add: `using Microsoft.AspNetCore.Mvc.ApiExplorer;` if we don't already have it in our "StartUp.cs" class.

With this change in place, we can now update our `UseSwaggerUI` from:

```csharp
 app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "My Test API V1");
});
```

To:

```csharp
app.UseSwaggerUI(c =>
{
    foreach ( var description in provider.ApiVersionDescriptions )
        {
            c.SwaggerEndpoint( $"/swagger/{description.GroupName}/swagger.json", description.GroupName.ToUpperInvariant() );
        }
});
```

If we have been careful in making these changes, then we should be able to, once again, `dotnet run` our project from the VS Code terminal and navigate to swagger (`https://localhost:5001/swagger`) to see that our endpoints are now nicely versioned:

{{< imgproc api-ver-5 Resize "800x" "swagger" "Figure 5" />}}

But before we declare total victory, we might want to add a second version. Once again navigate to our "ValuesController". This time, add 

```csharp
[ApiVersion("2.0")]
```

Beneath where we had added `[ApiVersion("1.0")]` before. Save the change and re-run our API. After navigating to our now familiar swagger address we should see the new version available to us in the top right corner of the SwaggerUI.

{{< imgproc api-ver-6 Resize "800x" "swagger" "Figure 6" />}}

---

#### Summary

And that about does it. From here you can choose to version your controllers or endpoints however you like. Obviously there are many more considerations about how to structure, organize, and version your code. We have only scratched the surface in this walkthrough. But the nice part about using the *microsoft-api-versioning* library is that it supports you, no matter how you choose to approach versioning whether that is 

* Query string parameter versioning

* URL path versioning (as in this example)

-or-

* Header versioning 

So, now that you have a basic working example, experiment with it to find the strategy that is right for your needs.

Thanks for reading.

---

You can find my [sample here](https://github.com/tsadams1973/dotnet-core/tree/master/api-ver) if you want a bit of a head start.
