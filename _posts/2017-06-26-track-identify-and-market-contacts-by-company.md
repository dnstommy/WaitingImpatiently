---
layout: post
title: "Track, Identify and Personalize Visitors by Company"
date: 2017-06-26
tags: [xDB, Personalization]
featured: true
reading_time: 5
---

This article explains how B2B companies can identify website visitors and personalize their experiences. Using IP tracking services like Kickfire and Maxmind to identify companies visiting a website.

## Core Concept

In B2B scenarios, identifying visitors enables targeted marketing and journey tracking through methods including email campaigns, cookie tracking, traditional marketing campaigns, and IP tracking.

## Implementation via Kickfire Module

The solution leverages the Kickfire Analytics Module for Sitecore to capture company data. When users visit, their IP addresses are passed to the Kickfire API, which returns detailed company information including name, location, employee count, revenue, industry classification, and social media profiles.

This company data integrates into Sitecore's xDB (experience database) and appears in the Experience Analytics interface, showing a company column in visit lists and allowing marketers to analyze engagement by organization.

## Personalization Features

**Company-Based Targeting:** Custom conditional rendering rules enable content personalization based on specific company names using string comparisons (equals, contains, begins with, etc.).

**Industry Personalization:** The SicCode from API responses maps to industries through a local SQL table, activating industry pattern cards. This allows content targeting by sector—for example, personalizing for "Educational Services" companies.

**Search Enhancement:** The contact search function now supports filtering by company name alongside contact names and emails.

## Technical Requirements

The solution requires Sitecore 8.2 and above and uses Microsoft Dependency Injection. The code is available on GitHub at the Bonfire-Company-Personalization repository.
