---
layout: post
title: "Add your xConnect facet to Experience Profile, the Lazy Way"
date: 2019-07-10
tags: [xDB, xConnect, Sitecore]
reading_time: 2
---

The challenge of displaying xConnect facets in Sitecore's Experience Profile traditionally involves complex, time-consuming processes. I discovered a faster solution using the EP Express Tab, an open-source Sitecore project that enables adding tabs to Experience Profile in approximately 10 minutes.

The implementation involves three main steps:

## Step 1: Add the NuGet Package

Install the EPExpressTab NuGet package to begin development.

## Step 2: Create a Model and View Model

Build a model to hold your facets and other necessary data. Then construct a view model extending the EpExpressViewModel class, which specifies the CSHTML view location for the EP tab.

## Step 3: Design the CSHTML View

Create the presentation layer injecting into the new EP tab. I incorporated Sitecore's styling to maintain visual consistency with Speak.

## How It Works

EP Express Tab automatically detects classes inheriting EpExpressViewModel and generates corresponding tabs in the core database. The tab naming derives from the TabLabel property, and the rendering automatically integrates into Experience Profile's presentation details.

For multiple tabs, developers simply create additional view models and views. The tab ordering can be adjusted within the core database at `/sitecore/client/Applications/ExperienceProfile/Contact/PageSettings/Tabs/`.
