---
layout: post
title: "NuGet packages.config is so yesterday"
date: 2018-10-22
tags: [Sitecore, Development]
reading_time: 3
---

NuGet's packages.config approach is outdated. PackageReference is the modern alternative. I discovered that Sitecore's HabitatHome.Commerce project no longer uses packages.config files, instead embedding NuGet references directly in project files.

## Benefits of PackageReference

This approach allows Sitecore to build DLLs independently rather than locking all components to a single version number. Developers can select specific DLLs and ignore dependencies using the PrivateAssets attribute.

Key improvements include:
- Automatic package restoration during builds
- Simplified package updates (just modify version numbers in the project file)
- Easier project initialization with code snippets
- Conditional references based on build configurations

## Example

Instead of the old two-step process (packages.config plus project references), use a single line:

```xml
<PackageReference Include="Sitecore.Kernel" Version="9.1.0">
  <PrivateAssets>all</PrivateAssets>
</PackageReference>
```

This streamlined approach represents the new recommended standard for Sitecore NuGet dependencies.
