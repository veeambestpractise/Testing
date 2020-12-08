---
title: Teams
parent: Use Cases
grand_parent: Operate
nav_order: 200
has_toc: false
---
# Microsoft Teams
Microsoft Teams is a colaboration software which uses all services of Microsoft Office 365 within one Client.

## Architecture
The logical Teams architecture is shared over following services:

| Data Source        | Data Storage(s)                            |
|--------------------|--------------------------------------------|
| Chat               | Exchange / Skype communications            |
| Personal Chatfiles | Personal OneDrive                          |
| Team-Chat          | SharePoint / O365 Groups / Exchange        |
| Team-Chat-Files    | SharePoint (Folder per Team / Sub-Channel) |
| Calendar           | Exchange                                   |
| Contacts           | Exchange                                   |
| Wiki               | SharePoint                                 |

## Backup
If you plan to backup MS Teams and want to create another copy of your backup-data ([3-2-1 rule](../../design/3-2-1) with Veeam Agent for Windows or Veeam Backup & Replication) please be aware that your backup of all services (Mail, SharePoint, OneDrive) should be scheduled close to each other.  

For example:
* Mail-Backup: 22:00
* SharePoint-Backup: 23:00
* OneDrive-Backup: 01:00
* Agent-Backup: 00:00
The result would be that the Agent backup at midnight does not include the OneDrive backup.

## Recovery
Due to the complex and shared environment behind Microsoft Teams we need to combine our restore capabilites with existing Veeam Explorer for Mail/Sharepoint/Onedrive
The data that is going to be restored is spread over the different Microsoft Office 365 services and can be found here:

| Data to be restored         | Restore Path                                                                             |
|-----------------------------|------------------------------------------------------------------------------------------|
| Chat / Conversation History | Veeam Explorer for Exchange -> Usermailbox -> Subfolder "Conversation History\Team Chat" |
| Chat-Files                  | Veeam Explorer for Onedrive -> Useraccount -> "Microsoft Teams Chat Files"               |
| Team Channel-Files          | Veeam Explorer for Sharepoint -> "Teams name" -> "Documents" -> "Channel"                |
| Team Wiki                   | Veeam Explorer for Sharepoint -> "Teams name" -> "Teams Wiki Data" -> "Channel"          |
| Calender                    | Veeam Explorer for Exchange -> "Usermailbox" -> Calender                                 |
    
Please be aware that all recoveries of objects (File, Wiki, OneNote) can not be recovered directly to Microsoft Teams today. A file can be directly restored in the associated SharePoint, but it won't re-appear in MS Teams that way.
The following describes the way how to restore to have objects available in Teams as expected:

* File: Download file or folder from Veeam Explorer for SharePoint / OneDrive -> Upload them to Microsoft Teams with the Microsoft Teams Client or Web-Application.
* Wiki: Open *.mht-File with Veeam Explorer for SharePoint -> Copy&Paste text to new Wiki in Microsoft Teams.
* OneNote: Download the OneNote-file from Veeam Explorer for SharePoint -> Upload file to Microsoft Teams with the Microsoft Teams Client or Web-Application.

            

       
