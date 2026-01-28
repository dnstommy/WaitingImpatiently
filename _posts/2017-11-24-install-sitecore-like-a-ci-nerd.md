---
layout: post
title: "Install Sitecore like a CI nerd. In minutes."
date: 2017-11-24
tags: [Sitecore, CI]
featured: true
reading_time: 2
---

I leverage community tools to expedite Sitecore 9 installation on development machines. While the SIF tool provides comprehensive configuration options, it lacks developer-friendly simplicity.

## The Tools

Three key utilities streamline the installation process:

**1. Low Effort SOLR** - Jeremy Davis's script automates SOLR setup from Apache, configures SSL, and enables the service within approximately two minutes.

**2. SIF-less** - Rob Ahnemann's tool simplifies Sitecore 9 installation by generating PowerShell scripts. Users can either fill in configuration fields or allow the tool to handle the installation directly.

**3. Chocolatey** - Described as "NuGet for applications," this package manager enables scripting and deployment of multiple applications simultaneously.

The combined approach yields a functioning Sitecore 9 installation in roughly 12 minutes, with variations based on hardware specifications.

## Machine Setup Prerequisites

The demonstration uses Windows 10 with:
- IIS and ASP.NET 4.7 features enabled
- SQL Server 2016 SP1 Express (default instance configuration)
- SQL Management Studio 17.3

A Chocolatey script installs development essentials: Chrome, Java Runtime, Git, .NET Core, Node.js, Visual Studio 2017, and additional utilities.

Optional Visual Studio Code extension installations enhance development workflows.
