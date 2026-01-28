---
layout: post
title: "Are you losing your xDB data?"
date: 2020-02-06
tags: [Sitecore, xDB, xConnect]
featured: true
reading_time: 2
---

If you are on Sitecore 9.0 to 9.1.1 without patches, data loss may occur. Users should watch for specific error messages in their logs.

## Expected Errors in Sitecore Logs

The system generates a message stating "ERROR General error when submitting contact. Exception: Sitecore.XConnect.Operations.FacetOperationException Message: Operation #0, AlreadyExists, <ContactId>, Classification Source: Sitecore.Xdb.Common.Web"

## Expected Errors in xConnect Logs

Similar FacetOperationException errors appear, indicating batch execution problems with contact classification operations.

## Official Solution

A patch exists in the Sitecore Knowledge Base addressing this contact-saving issue.

## Persistent Problem in Multi-Server Environments

Even with the patch installed, errors continue in specific configurations:
- Multiple Content Delivery servers
- Load balancer implementation
- Session state stored in-process (not Redis, MongoDB, or SQL)

## Root Cause

When clients switch between servers or devices, in-process sessions disconnect, severing the contact reference. New sessions attempting to save contacts generate duplicate operation errors.

## Resolution

Move both shared and private session state to Redis, SQL Server, or MongoDB using Sitecore's official configuration walkthroughs.

**Note:** SQL implementations won't function in Azure SQL due to temp database requirements.
