---
title: Minimums
parent: Installation 
has_children: true
nav_order: 130
has_toc: false
---

# This section covers the minimum specification that should be in place.

## You will need three server roles at a minimum to start to use Veeam Backup for Office 365:  

* Cloud Connect Server/VBO Server
* Cloud Gateway
* Backup for Office365 Proxy server

The minimum specification should be as follows:

| Role                                                 | CPU*   | RAM(GB)*   | Disk Usage(GB)  | Network     | SQL        |
---:|:---:|:---:|:---:|:---:|:--- 
| **Cloud Connect Server/VBO Server** | 8          |12                |100                     |Management  | SQL Express|
| **Cloud Gateway**|2|4|64|DMZ|  |
| **Backup for Office 365 Proxy** | 4|8|Disk 1: 64 |Management of O365 Proxy Network|   |
|   |   |   |  Disk 2: **| | |


*These Figures are recommended minimums only

**Disk 2 will be used to store O365 Metadata for each tenant. The Capacity required wqill be based on the total protected capacity


Using these  numbers we can estimate the following consumption and requirements :

|Number of Users | Estimated Number of Objects| Proxy CPU Requirement| Proxy Ram Specified|
---:|:---:|:---:|:---:|
| 750 | 1943  | 4 | 8 |
|6000| 15040|8|32|