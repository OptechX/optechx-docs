---
title: Enable Swagger
author: optechx
date: 2019-09-10 09:17:00 +1000
categories: [Template, Swagger]
tags: [swagger,template]
pin: true
math: true
mermaid: true
image:
  path: https://chirpy-img.netlify.app/commons/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

## Install Swashbuckle.AspNetCore
Use NuGet Package Manager or .NET CLI to install the Swashbuckle.AspNetCore package. Open a terminal or command prompt, navigate to your project directory, and run the following command:

```bash
dotnet add package Swashbuckle.AspNetCore
```

## Configure Swagger in Program.cs
Modify your `Program.cs` file as follows to configure Swagger:

```csharp
using Microsoft.AspNetCore.Components.Web;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.AspNetCore.Builder;
using Microsoft.OpenApi.Models;
using Microsoft.AspNetCore.Hosting;

namespace ProjectName
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var builder = WebApplication.CreateBuilder(args);

            // Add services to the container.
            builder.Services.AddRazorPages();
            builder.Services.AddServerSideBlazor();
            builder.Services.AddSingleton<WeatherForecastService>();

            // Configure Swagger services
            builder.Services.AddSwaggerGen(options =>
            {
                options.SwaggerDoc("v1", new OpenApiInfo
                {
                    Title = "ProjectName API",
                    Version = "v1"
                });
            });

            var app = builder.Build();

            // Configure the HTTP request pipeline.
            if (!app.Environment.IsDevelopment())
            {
                app.UseExceptionHandler("/Error");
            }

            app.UseStaticFiles();

            app.UseRouting();

            app.MapBlazorHub();
            app.MapFallbackToPage("/_Host");

            // Enable middleware to serve generated Swagger as a JSON endpoint
            app.UseSwagger();

            // Enable middleware to serve Swagger UI
            app.UseSwaggerUI(options =>
            {
                options.SwaggerEndpoint("/swagger/v1/swagger.json", "ProjectName API V1");
            });

            app.Run();
        }
    }
}
```

## Generate Swagger Documentation
Build your Blazor Server project ot generate Swagger documentation. Ensure that you have endpoints or controllers in your application that Swagger can document.

## Launch Application
Run your Blazor Server application. YOu can access teh Swagger UI by navigating to `https://yourdomain.com/swagger`. This code will integrage Swagger into your Blazor Server application, allowing you to document and explore your API endpoints interactively using Swagger UI. Make sure to replace `"ProjectName"` with an appropriate title in the Swagger configuration.