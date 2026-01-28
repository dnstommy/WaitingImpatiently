---
layout: post
title: "Moving controllers routes into Sitecore"
date: 2016-03-01
tags: [Sitecore]
reading_time: 1
---

I traditionally registered custom API controllers in Sitecore by modifying the Global.ascx.cs file, similar to standard ASP.NET MVC practices. However, when deploying packages to customer applications, overwriting the Global.ascx file becomes problematic.

## The Solution

To solve this, I leverage Sitecore's pipeline architecture. Create a processor inheriting from `Sitecore.Mvc.Pipelines.Loader.InitializeRoutes` that handles route registration:

```csharp
public class RegisterRoutes : InitializeRoutes
{
    public override void Process(PipelineArgs args)
    {
        RouteTable.Routes.MapRoute(
            "Profile",
            "VisitorData",
            new { controller = "Visitor", action = "VisitorDetailsJSON" },
            new[] { "MyCompany.Analytics.Controllers" }
        );
    }
}
```

## Configuration

The processor is integrated into Sitecore's initialization pipeline via XML configuration. **Important:** Patching must occur *before* the default `Sitecore.Mvc.Pipelines.Loader.InitializeRoutes` processor. Failing to maintain this order causes `Tracker.Current` object to become null, potentially disrupting Experience Tracker API functionality.

```xml
<configuration>
  <sitecore>
    <pipelines>
      <initialize>
        <processor type="MyCompany.RegisterRoutes, MyCompany"
                   patch:before="processor[@type='Sitecore.Mvc.Pipelines.Loader.InitializeRoutes, Sitecore.Mvc']" />
      </initialize>
    </pipelines>
  </sitecore>
</configuration>
```
