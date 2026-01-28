---
layout: post
title: "Shipping Sitecore Errors to Sentry.io"
date: 2017-08-12
tags: [Sitecore, ALM, Logging]
reading_time: 1
---

Effective Sitecore application lifecycle management requires awareness of application errors and whether new deployments introduce issues. Simple up/down monitors or other online tracking may miss sporadic problems, making error log shipping and alerting critical for reliability.

## What Sentry.io Does

Sentry.io functions as an error tracking service that can gather up error messages, tell you where they are happening, when, and on which browsers. Additional capabilities include tracking user behavior through breadcrumbs and logging supplementary environment data for developers debugging production issues.

## Implementation Overview

The solution involves three components:

1. **NuGet Packages** - Adding appropriate dependencies to the project
2. **CustomAppender Class** - A new class to handle the integration
3. **Sitecore Configuration** - Creating a log4net appender with filtering to send only error-level events to Sentry.io

The configuration approach uses a filter attribute to ensure only errors reach the new appender, while the existing Sitecore logger continues functioning normally. A root patch adds the second appender to the main Sitecore logger.

*Credit: JammyKam for assistance in developing this solution.*
