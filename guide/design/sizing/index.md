---
title: Sizing
parent: Design
nav_order: 400
has_toc: false
has_children: true
---
# Sizing

## Users and Objects
Sizing VBO is based on number of objects rather than the number of users to protect or the actual size of the organisation. This is because a user can have access to multiple objects. The objects list include:

**For Exchange Online and On-Premises**
- Primary Mailbox
- Archive Mailbox
- Shared Mailboxes
- Public MailFolders
- Exchange Resources (Room, Equipment)

**For SharePoint Online and On-Premises**
- Sites (Collaboration, Communication, Publishing, Enterprise, Template based)
- Personal Sites
- Teams Sites

**For OneDrive for Business Online and On-Premises**
- OneDrive accounts


**Use case**: Organization with **500** users might need to protect all mailboxes (Primary and Archive) **200** Shared Mailboxes, **10** Public MailFolders, all Personal Sites and OneDrives along with **1000** SharePoint sites. The total number of objects amounts to **3,210** objects as per table below:

| Value    | Type                  |
|----------|-----------------------|
| **500**  | Primary Mailboxes     |
| **500**  | Archive Mailboxes     |
| **200**  | Shared Mailboxes      |
| **10**   | Public MailFolders    |
| **500**  | Personal Sites        |
| **500**  | OneDrive for Business |
| **1000** | SharePoint Sites      |

The backup and restores are executed by the Veeam VBO proxies and the best practice is to not exceed **4,000** users per proxy. Considering the main 4 object types (Mail, Archive, Site, OneDrive) each VBO proxy can protect up to **16,000** objects and since we allow up to 10 proxies per VBO server, each VBO installation can protect up to **160,000** objects. When configuring VBO Backup jobs these should not exceed the mentioned object numbers for optimal performances.

### How to size the backup jobs
When sizing the backup jobs the best practise includes the following:
- Create separate jobs based on the application type (eg. separate jobs for Exchange, SharePoint and OneDrive). This also allows to direct the jobs to different repositories with separate retention. Different types of data don't grow equally.
- Do not exceed the 4,000 users per job.
- For large environments it is advised to increase the retry fail in the job configuration at least to 20 minutes or more.
- Run the backup jobs outside the work hours reducing impact on Microsoft Office 365 throttling when other clients (OneDrive, ActiveSync etc..) are operating.

## Proxy Servers
VBO Proxy sizing depends on the total number of objects to protect. Each VBO Server instance supports up to 10 VBO Proxies. Each VBO Proxy then supports up to 16,000 objects as any combination of Mail, Archive, Site and OneDrive. More information are available in the Configuration Maximums section.

When sizing the VBO Proxies there are two important VBO parameters to know about:
- Number of threads
- Amount of bandwidth

### Number of threads
It is the number of active connections started by the VBO Proxy responsible for backing up data. This number goes from 0 to 256. The higher the number the faster potentially the backup job will complete. Default number of VBO Proxy connections is 64. Although it is possible to change this number, using a thread number too high might incur in the Throttling Policy that Microsoft Office 365 activates to control the resources external clients/connection require. The advice is to monitor same sample "test jobs" to verify and adjust the number of threads.

### Amount of bandwidth
Represents the network throughput shared across the number of configured threads. By default is set to unlimited. In this case all the available bandwidth to the server running as VBO Proxy will be used. The best practice is to limit the maximum amount of bandwidth the VBO Proxy can use. It is interesting to note the VBO Proxy might not necessarily use the maximum bandwidth configured as this also depends on the Office 365 throttling limiting the connection speed. In any case the bandwith is always shared across the number of threads.
