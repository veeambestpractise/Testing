---
title: Proxy & Repository Server
parent: Build & Configure
has_children: true
nav_order: 200
has_toc: false
---

# Proxy & Repository Server

Repositories are tightly coupled with proxy servers. While a single proxy server can host multiple repositories, each repository
is uniquely coupled with a single proxy server.

Repositories can reside on Direct Attached Storage (DAS), Storage Area Network (SAN) volumes or on a SMB3 Network Attached Storage
(NAS) share and contain Microsoft Jet databases (`.adb`).

From v4 of the product object storage repositories are also supported. For these only a small cache is used locally
(usually ~1% of the whole repository size) and all other content is directly stored in the object storage bucket/container.
For one repository you can either use local block storage or object storage. There is no tiering functionality in between these storage types as in VBR.

## Best Practice Notes

### Disk Repository

- Use high throughput low latency storage. Thus **DAS or SAN** are preferred storage volumes for repository.
  Go with the default controller and stripe size settings.
- Repository **File System** should be chosen as **NTFS** with default settings (4k allocation units).
- Do **not enable storage encryption, dedup or compression** on the repository volume for better performance
- **Separate repositories by data type** (Exchange, OneDrive, SharePoint) to allow higher flexibility based on the different data-change characteristics
- **Avoid very large repositories** because handling them gets harder. Distribute the backup data over several repositories, e.g. split by business units
- Keep **10% free working space** per repository to avoid lock downs

### Object Storage Repository

- General security best practices apply - create an own storage user with own credentials for the bucket/container, apply restrictive ACL
- Do **not setup tiering policies** on the object storage side. This is not supported and will break things.
- Do **not manually delete** anything from the object storage bucket/container, unless you don't want to use the repository anymore (then you can delete everything)
- Provide disk space for **~1% of your source data size as local cache**. In case of restores this local cached metadata reduces the need of 90% of the required API calls to the object storage (which might incurr cost on public cloud)

### Proxy

- **Throttle** the used **bandwidth** per proxy **on a shared network** connection to not block other applications

## [More in-depth information on this item](proxy-repo-details.md)

## External Resources

- [Veeam HelpCenter - Veeam Backup for Microsoft Office 365 User Guide](https://helpcenter.veeam.com/docs/vbo365/guide/)
  - [Backup Proxy Servers](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_backup_proxy_servers.html)
  - [Backup Repositories](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_backup_repositories.html)
