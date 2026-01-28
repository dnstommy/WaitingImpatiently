---
layout: post
title: "Reseting the admin password to b"
date: 2016-01-18
tags: [Sitecore, SQL]
reading_time: 1
---

To reset the admin password to 'b' via SQL, run the following SQL on the **core database**:

```sql
UPDATE [aspnet_Membership]
SET
    Password = 'qOvF8m8F2IcWMvfOBjJYHmfLABc=',
    PasswordSalt = 'OM5gu45RQuJ76itRvkSPFw==',
    IsApproved = 1,
    IsLockedOut = 0
WHERE UserId IN (
    SELECT UserId
    FROM aspnet_Users
    WHERE UserName = 'sitecore\Admin'
)
```

This resets the Sitecore admin account password to the letter "b" and ensures the account is approved and not locked out.
