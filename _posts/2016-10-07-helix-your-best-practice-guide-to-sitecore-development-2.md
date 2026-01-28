---
layout: post
title: "Helix: Your Best Practice Guide to Sitecore Development"
date: 2016-10-07
tags: [Sitecore]
reading_time: 3
---

Sitecore is a dynamic and configurable content management system. However, its openness creates challenges, as developers can approach Sitecore implementation in numerous ways, leading to ongoing debates about best practices.

Sitecore has addressed this by releasing Helix, described as "a set of overall design principles and conventions for Sitecore development." Complementing Helix is Habitat, a fully functional Visual Studio project demonstrating Helix principles. Important: **use Habitat as a guideline for development, but DO NOT use it in production.**

## Layers Architecture

Helix's core concept involves three architectural layers:

**Project Layer:** Site-specific assets including layouts, renderings, templates, and settings unique to individual sites in multisite environments.

**Feature Layer:** Shared functionality organized around business requirements rather than technical ones. Each feature should be self-contained, including all necessary Sitecore items, controllers, views, and code. For example, a navigation feature should be named "Navigation" rather than "Main Navigation."

**Foundation Layer:** The solution's core infrastructure containing shared libraries, base Sitecore items, and foundational renderings. Features should depend only on the Foundation layer, never on other features.

## Getting Started

I recommend downloading Habitat to understand the architecture firsthand. For new projects, the Yeoman generator "generator-prodigious-helix" provides Visual Studio scaffolding, though it currently supports TDS with potential future Unicorn support.
