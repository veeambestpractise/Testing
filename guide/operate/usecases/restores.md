---
title: Restores
parent: Use Cases
grand_parent: Operate
nav_order: 100
has_toc: false
---
# Restores 

Veeam Backup for Microsoft Office 365 provides multiple options to restore the objects with Veeam Explorers.

## Restore to another tenant

To restore or migrate the mailbox to an alternative tenant, follow the steps below:

- Open Veeam Explorer for Exchange
- Export the mailboxes as PST files.
- Go to [https://protection.office.com](https://protection.office.com) and sign in using the credentials for an administrator account in your Office 365 organization.
- Go to *Security & Compliance Center*, click *Data Governance* > *Import*.
- On the import page, click *New import job*.
- Select the upload data option.
- Upload the data to Office 365 and map it to the users.

For more details on this procedure, please check the [Microsoft documentation](https://docs.microsoft.com/en-us/microsoft-365/compliance/use-network-upload-to-import-pst-files).