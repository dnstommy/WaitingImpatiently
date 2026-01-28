---
layout: post
title: "Intellisense Issue When Using Sitecore Local NuGet Files"
date: 2016-01-19
tags: [Sitecore]
reading_time: 1
---

The Sitecore Instance Manager (SIM) tool introduced local NuGet support, eliminating the need to manually manage library folders and track DLL versions. However, users implementing this feature encountered a problem: when I used the new DLLs, all my intellisense went away.

## The Solution

Thanks to Jammy Kam via the Sitecore Slack community, the solution involves a straightforward configuration change:

Adjust each Sitecore DLL's properties within Visual Studio, setting **CopyLocal to `true`**.

This simple modification restores intellisense functionality.

## Important Note

If using Team Development for Sitecore (TDS) for package management, these DLLs must be excluded from the deployment package to prevent duplication.
