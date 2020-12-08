---
title: Organization Config
parent: Operate
nav_order: 90
has_toc: false
---
# Organization Configuration

## Backup Accounts
When handling a lot of SharePoint Online or OneDrive for Business backups you might encounter the Microsoft Office 365 throttling mechanism.
To counter this mechanism, which works on a per user basis, you can configure multiple backup accounts in VBO which are used to backup the data.

If you encounter throttling, start adding 8 accounts per proxy for the organization and increase by increments of 8 until throttling disappears.

To help creating and adding accounts have a look at the blog of Niels Engelen who created a [PowerShell scrip to automate adding backup accounts](https://foonet.be/2020/01/03/veeam-backup-for-microsoft-office-365-adding-auxiliary-backup-accounts-via-powershell/)