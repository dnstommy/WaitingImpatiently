---
layout: post
title: "Are Your Salesforce Admins Ready for Phishing-Resistant MFA?"
date: 2026-06-12
tags: [Salesforce]
reading_time: 5
---

Salesforce's July 2026 enforcement deadline is approaching fast: admins and privileged users will be required to use **phishing-resistant MFA** — not just any second factor. A YubiKey or a platform authenticator like Windows Hello or Touch ID qualifies. A Salesforce Authenticator push notification or a TOTP code from Google Authenticator does not.

If you haven't audited your org yet, here's exactly how to do it.

## What counts as phishing-resistant?

Salesforce tracks two phishing-resistant methods:

- **`HasSecurityKey = true`** — a registered WebAuthn security key. This includes hardware keys (YubiKey, etc.) as well as synced passkeys from iCloud Keychain, 1Password, or Bitwarden, as long as the manager is FIDO2/WebAuthn-compliant.
- **`HasBuiltInAuthenticator = true`** — a registered platform authenticator (Windows Hello, Touch ID, or Face ID bound to that device).

Standard MFA methods — `HasSalesforceAuthenticator` and `HasTotp` — do not satisfy the phishing-resistant requirement and will trigger a step-up prompt at login after the enforcement date.

## Step 1: Create the "MFA API Access" permission set

The `TwoFactorMethodsInfo` object requires elevated permissions to query. Create a permission set that grants them.

1. Go to **Setup → Permission Sets → New**
2. Name it **MFA API Access**, leave the license blank
3. Open **System Permissions**
4. Enable **Manage MFA in API** and **Manage MFA in User Interface**
5. Save, then assign the permission set to your user via **Manage Assignments**

Without this, the SOQL query below will return a `INSUFFICIENT_ACCESS` error.

## Step 2: Run the audit query

Open the **Developer Console** or use **Workbench** and run:

```sql
SELECT User.Username, User.Profile.Name,
       HasBuiltInAuthenticator, HasSecurityKey, HasU2F,
       HasSalesforceAuthenticator, HasTotp
FROM TwoFactorMethodsInfo
WHERE User.IsActive = true
```

This gives you a row per active user who has registered at least one verification method, showing exactly which factors each person has in place.

## Step 3: Find who isn't ready

Narrow the results to users who have no phishing-resistant method registered:

```sql
SELECT User.Username, User.Profile.Name,
       HasBuiltInAuthenticator, HasSecurityKey, HasU2F,
       HasSalesforceAuthenticator, HasTotp
FROM TwoFactorMethodsInfo
WHERE User.IsActive = true
  AND HasBuiltInAuthenticator = false
  AND HasSecurityKey = false
```

Anyone returned here would hit the step-up wall after July enforcement. Tighten the scope to the highest-risk profiles:

```sql
SELECT User.Username, User.Profile.Name,
       HasBuiltInAuthenticator, HasSecurityKey, HasU2F,
       HasSalesforceAuthenticator, HasTotp
FROM TwoFactorMethodsInfo
WHERE User.IsActive = true
  AND HasBuiltInAuthenticator = false
  AND HasSecurityKey = false
```

To focus on admins specifically, cross-reference the results against a User query filtered by `Profile.Name = 'System Administrator'`. Do the same for any profiles or permission sets granting Modify All Data or Manage Users — those users carry the same risk as sysadmins.

## Two caveats you need to know

**Users with zero methods won't appear.** A row only exists in `TwoFactorMethodsInfo` once a user has registered *something*. Users who have never set up any MFA at all are silently absent. Cross-check your query results against a full active-admin list (`SELECT Username FROM User WHERE IsActive = true AND Profile.Name = 'System Administrator'`) to catch anyone missing entirely.

**Legacy U2F is a gray area.** `HasU2F` (flagging keys registered under the old FIDO U2F protocol) is tracked separately from `HasSecurityKey` (WebAuthn). If anyone has a legacy U2F registration, it's safer to have them re-register under WebAuthn rather than assume Salesforce will honor it toward the phishing-resistant requirement. Hardware keys like YubiKeys support both; the re-registration takes about a minute.

## What to do with the results

Once you have your at-risk list:

1. **Choose a method for each user.** Platform authenticators (Windows Hello, Touch ID) are zero-cost and built into devices most admins already use. Hardware keys are the better fit for shared workstations or users who move between machines.
2. **Have users register before the deadline.** Walk them through **Setup → Advanced User Details → Register** under the Security Key or Built-In Authenticator section.
3. **Re-run the audit query** after registration to confirm `HasSecurityKey` or `HasBuiltInAuthenticator` flipped to `true`.
4. **Don't forget service/API users.** Automated integrations authenticating as admin users need certificate-based or OAuth flows that don't require interactive MFA — make sure those are in place before enforcement hits.

The query takes two minutes to run. The harder part is the follow-up with users who've been putting off the upgrade. Give them a specific deadline a week before Salesforce's, so you have buffer to resolve stragglers before the forced step-up affects production access.
