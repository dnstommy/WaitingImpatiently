---
layout: post
title: "Enabling flows for Salesforce Integration user"
date: 2025-05-15
tags: [Salesforce]
reading_time: 2
---

The Salesforce Integration user license provides an economical option for system-to-system integrations but arrives with significant constraints. Most notably, these users cannot execute Flows by default—a limitation that can obstruct automation efforts.

However, the restriction can be overcome through strategic permission configuration. The process involves five steps:

## Step 1: Create Permission Set

Establish a new permission set titled "Integration Permission Set" with no assigned license.

![Create Permission Set with no license assigned](/assets/images/salesforce-integration-flows/image.png)

## Step 2: Create Integration User

Set up a dedicated user with the "Salesforce Integration" license and assign the "Salesforce API Only System Integration" profile.

## Step 3: Assign Permission Set License

This represents the critical phase. The Salesforce API license defaults to severe restrictions. Navigate to "Permission Set License Assignments" and enable the "Salesforce API Integration" license—this restores standard functionality.

![Permission Set License Assignments section](/assets/images/salesforce-integration-flows/image-1.png)

![Enable Salesforce API Integration license checkbox](/assets/images/salesforce-integration-flows/image-2.png)

## Step 4: Enable Run Flows Permission

Access the Integration Permission Set's App Permissions section and activate the "Run Flows" checkbox.

![App Permissions link in Integration Permission Set](/assets/images/salesforce-integration-flows/image-3.png)

![Run Flows checkbox in App Permissions](/assets/images/salesforce-integration-flows/image-4.png)

## Step 5: Assign Permission Set to User

Complete the configuration by assigning your newly created permission set to the integration user through the Manage Assignments button.

![Manage Assignments button in Permission Set](/assets/images/salesforce-integration-flows/image-5.png)

**Note:** Without enabling the permission set license in Step 3, attempting to assign the permission set generates an error message regarding incompatible user licenses.
