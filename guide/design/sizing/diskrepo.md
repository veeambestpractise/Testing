---
title: Disk Repository
parent: Sizing
grand_parent: Design
nav_order: 100
has_toc: false
---
# Disk Repository

The sizing for the local disk repositories (DAS, SAN, NAS) differs based on the stored data. The given formulas are based on experiences but dependent on your individual data the real usage can vary.

## Exchange Data
The given formula applies to both item-level and snapshot based repositories.

**For primary mailboxes**
```
(Current primary mailboxes total size) + ((Daily change rate * 2) * (Days of retention)) + (10% working area)
```

**For archive mailboxes**
```
(Current archive mailboxes total size) + ((Daily change rate) * (Days of retention)) + (10% working area)
```

If you run an existing O365 or on-premise Exchange use the PowerShell commandlets `Get-Mailbox` and `Get-MailboxStatistics` on your infrastructure to get input to the following formulas.

You can get the *Total size of current primary mailboxes* with `Get-Mailbox` and *Total size of current archive mailboxes* with `Get-Mailbox -Archive`.

The following example returns the size of all primary mailboxes and can be adapted for archive mailboxes using the `-Archive` option:

```PowerShell
Get-Mailbox | Get-MailboxStatistics | Select-Object DisplayName, ItemCount, TotalItemSize | Format-Table –autosize
```

In the field we experience typical daily change rates from 0.2 to 1%. For normal mailbox backups the change rate is multiplied by 2 because of archiving and file versioning which takes up additional backup space. More optimistically this factor can be also calculated with 1.5.

While processing the backups transaction protocols and database checkpoints can take up to 10% of the repository space which is calculated as the workspace.

## SharePoint and OneDrive Data
You can view current and previous data usage for SharePoint Online and OneDrive for Business in the Office 365 Admin Center, e.g. for SharePoint at *Reports > Usage > SharePoint > Site Usage > Storage*.

With this data you can estimate the daily change rate and the total data size. Consider this total data size to be the planned size in the future depending on for how long you size your backup infrastructure.

The formula for SharePoint and OneDrive data is the same (OneDrive for Business is basically SharePoint under the hood).

```
(Total data size) + ((Daily change rate) * (Days of retention)) + (10% working area)
``` 

From our field experience we see daily change rates of about 0.5 to 1%.

To limit the overall backup size you can reduce the number of item versions in document libraries and lists.