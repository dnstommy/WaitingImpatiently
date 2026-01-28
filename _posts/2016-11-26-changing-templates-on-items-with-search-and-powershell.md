---
layout: post
title: "Changing templates on items with search and powershell"
date: 2016-11-26
tags: [Sitecore, PowerShell]
reading_time: 2
---

I encountered a production issue where a deployment change had released several items to production where newly created content folders were of the wrong template type.

Rather than crawling the entire content tree from /Sitecore/Content, the solution leveraged the `Find-Item` function to query the Sitecore index. Results from Find-Item are of type `Sitecore.ContentSearch.SearchType.SearchResultItem`.

## The Solution

To resolve the template mismatch, the process involved two steps:

1. Retrieve items using `Get-Item $id`
2. Apply the `ChangeTemplate` method to reassign the correct template

```powershell
$items = Find-Item -Index sitecore_master_index -Criteria @{Filter = "Equals"; Field = "_template"; Value = "wrong-template-id"}

foreach($item in $items) {
    $sitecoreItem = Get-Item -Path "master:" -ID $item.ItemId
    $newTemplate = Get-Item -Path "master:" -ID "correct-template-id"
    $sitecoreItem.ChangeTemplate($newTemplate)
}
```

## Resources

- [Sitecore PowerShell Extensions](https://marketplace.sitecore.net/en/Modules/Sitecore_PowerShell_console.aspx)
- [Find-Item documentation](https://sitecorepowershell.gitbooks.io/sitecore-powershell-extensions/content/appendix/commands/Find-Item.html)
