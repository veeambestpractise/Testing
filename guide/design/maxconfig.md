---
title: Configuration Maximums
parent: Design
nav_order: 500
has_toc: false
---
# Configuration Maximums
This section covers the supported VBO configuration maximums. Numbers might vary depending on deployments types and available resources. These values represent what's currently supported also in light of acceptable performance. The values provided refer to any combination of Online and On-Premises environments that use Microsoft Exchange, Microsoft SharePoint and OneDrive for Business.

The tables in this section use the number of objects and their variations as a metric for estimations.

## Object types and variations:

- Mail (Primary, Archive, Shared, PublicFolder)
- Sites (SharePoint, Personal, Teams)
- OneDrive for Business

## Supported Maximums

| Type                                                |     Value |
|-----------------------------------------------------|----------:|
| Maximum number of objects per Proxy [^1] [^2]       |    16,000 |
| Maximum number of Users per Job [^2]                |     4,000 |
| Maximum number of Users per Proxy [^2]              |     4,000 |
| Maximum number of Proxies per VBO installation      |        10 |
| Maximum number of objects per VBO installation [^2] |   160,000 |
| Maximum number of Users per VBO installation [^2]   |    40,000 |
| Maximum size per VBO Repository [^3] [^4]           | Unlimited |

The maximums per component (proxy, repo, installation) must be maintained at the same time (e.g. number per objects and number per users).

[^1]: Based on a Veeam Backup for Microsoft Office 365 proxy running with 8x CPUs and 32 GB RAM memory

[^2]: Selecting Mail, Archive, OneDrive and Sites object for each user

[^3]: The Veeam Backup for Microsoft Office 365 repository consists of multiple folders named after the number of years of retention. For each year folder there is a repository file (.adb) plus a transaction and check log (.jrs and .chk). The total supported size for each .adb file is 64 TB. For example, three-year retention creates three folders with backup files that can grow by up to 64 TB, with one .adb per folder

[^4]: An automatic rule triggers when repository database files reach 59 TB. At this point, a new repository database file is automatically created in the same storage location. This allows users to bypass the first limit.

## RAM allocation and number of Repository databases per Proxy

| Type                                                                                                 | Value               |
|------------------------------------------------------------------------------------------------------|---------------------|
| Default JET database instance memory consumption on Veeam Backup for Microsoft Office 365 repository | 0.1% of host memory |
| Default JET database engine memory cache(1)                                                          | 50% of host memory  |
| Recommended number of JET databases per backup proxy (with default settings)                         | 250                 |
| Max number of JET databases per backup proxy (with customised settings) [^5]                         | 700-750             |

[^5]: Contact Veeam support for advanced RAM memory allocation on Veeam Backup for Microsoft Office 365 proxies. For the default backup Proxy, consider allocating at least 15% of the host RAM for Veeam Backup for Microsoft Office 365 Server operations.
