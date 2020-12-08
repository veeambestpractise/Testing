---
title: More Details
grand_parent: Build & Configure
parent: Proxy & Repository Server
nav_order: 100
---
# Proxy & Repository Server Details

## Disk Repository

### Storage Volumes
Veeam Backup for Microsoft Office 365 (VBO) stores backup data in a Microsoft Jet database `.adb` file in the repository. As this means random I/O on the used storage a high IOPS and bandwidth storage is preferred. In general DAS or FC-SAN block storage is preferred over ISCSI or SMB based storage.

### File System
Both NTFS and ReFS file systems are supported. When using ReFS, the data integrity features should be disabled in particular for volumes where data folders are located or at least exclude VBO repository files. NTFS is recommended because it does not need any error-prone reconfiguration from the default settings.

Storage encryption, dedup or compression does always mean added latency on I/O requests, thus we recommend to disable these features for better performance.

### Separate Repositories
The maximum supported file size for the Jet DB database files (`.adb`) is 64TB. An automatic rule triggers when the repository database files reaches 59 TB at which point a new repository database file is automatically created in the same storage location. This allows to overcome the first limit.

However, handling such large repositories (e.g. for migration purposes) comes with problems like long migration times, handling very large file systems, etc. Thus we recommend to limit the maximum size of target repositories by separating the backup data to different repositories. Especially separation by data type (Exchange, OneDrive, SharePoint) is reasonable, as depending on the type the change characteristics (amount of data, changerate) are normally different.
While for Exchange a lot of objects might be changed, the amount of data is normally quite low, as most of it is just text. For OneDrive however, the average changed file size might be much higher because it is used to store large binary files.
Even for the same type of data (e.g. OneDrive) it might be reasonable to again separate this data only, e.g. by business unit, when the overall data size is very high.

### Working Space
Additional space for transaction protocols or database checkpoints is required per repository. There should always 10% free workspace per repository to compensate this.

## Object Storage Repository

### No Tiering Policy on Object Storage
Many object storage providers provide the possibility to configure tiering policies to move older objects from a high-cost/low-latency object storage to a low-cost/high-latency object storage, e.g. Amazon Glacier or Microsoft Cool Blob.

There is currently **no built-in support in Veeam Backup for Microsoft Office 365 for these kind of archive tiers** and the native tiering policies must not be configured because

* The archive tiers do use other APIs than the "normal" object storage. Data which is moved is not accessible anymore for VBO.
* Even old objects can still be part of the latest restore point. Think about a one year old email which is still in your inbox because it contains evergreen information. By tiering items older than a year to an archive tier, this mail would be inaccessible for Veeam while it is still expected to be part of yesterday's backup when a restore kicks in.

### Manual Deletion
Interfering with the Veeam managed retention of objects in the repository can break the consistency of backups and thus must be avoided.

### Local Cache
Read more detailled information in the sizing section for [Object Storage](../design/sizing/objectstorage)

## Proxy

### Bandwidth Throttling
By default the proxy servers will take all available bandwidth to run the backups as fast as possible. As normally there is no dedicated internet connection available just for VBO backup, it's reasonable to throttle the maximum usable bandwidth (which is done per proxy) so that other applications do not suffer (too much). Depending on the backup schedule the limit should be set to a reasonable value. It might be okay to take 90% of the bandwidth at night but if the backup runs during working hours only 40% can be consumed without affecting operations.
