---
title: Design
has_children: true
nav_order: 100
has_toc: false
---
# Design
Based on the needs of an organization Veeam Backup for Microsoft Office 365 can be deployed in different ways. Veeam Backup for Microsoft Office 365 can be installed in a single server setup for small environments or be scaled running on multiple servers to process bigger environments.  The implementation design of Veeam Backup for Microsoft Office 365 is based on four different components within the product.
-	Veeam Backup for Microsoft Office 365 Server
-	Veeam Backup for Microsoft Office 365 Proxy Servers
-	Veeam Backup for Microsoft Office 365 Repositories
-	Veeam Explorers

To scale the environment multiple proxies can be implemented (scale-out) and process multiple tasks in parallel. To store the backup data multiple repositories can be deployed and configured.

In contrast of Veeam Backup and Replication the Proxy Server and Repositories within Veeam Backup for Microsoft Office 365 are directly coupled. These are connected within a One-to-Many relationship. A Repository is connected to a single Veeam Backup for Microsoft Office 365 Proxy server. One Veeam Backup for Microsoft Office 365 Proxy server can handle multiple repositories.
