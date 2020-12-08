---
title: Tenants
parent:  Installation
nav_order: 115
has_children: true
has_toc: false
---
# Self Service and the Veeam Backup and Replication Server

Required Software for each tenent to use this service

Each Tenant will require access to two pieces of Veeam software to perform self-service restore operations. 
1.	A Veeam Backup and Replication Server 
2.	The installation of at least one Veeam Explorer.


## To configure Office 365 Backup as a Service for tenants, do the following:

1. Add a service provider in Veeam Backup & Replication, as described in the [Connecting to Service Providers](https://helpcenter.veeam.com/docs/backup/cloud/cloud_connect_sp.html?ver=100) section of the Veeam Cloud Connect Guide.
2. Add backups to the Veeam Explorer scope, as described in [Exploring Backups in Veeam Explorers](https://helpcenter.veeam.com/archive/vbo365/40/guide/vbo_vex_adding_store.html).


Make sure to install at least one of the below:
* Veeam Explorer for Microsoft Exchange
* Veeam Explorer for Microsoft SharePoint
* Veeam Explorer for Microsoft OneDrive for Business 

These come as part of the Veeam Backup for Microsoft Office 365 distribution package.

By default, tenants cannot restore anything without the service provider assistance. To be able to perform self-service recovery procedures, a service provider must configure authentication settings for tenants, as described in [Configuring Authentication Settings](https://helpcenter.veeam.com/archive/vbo365/40/guide/vbo_authentication_settings.html).

Tenants must provide service providers with their Microsoft organization credentials. Tenants can use the same credentials when adding a Veeam Backup for Microsoft Office 365 service provider server to the Veeam Explorers scope, as described in [Working with Backups in Veeam Explorers](https://helpcenter.veeam.com/archive/vbo365/40/guide/vbo_vex_adding_store.html).




Optionally, install a 64 bit version of Microsoft Outlook which provides for the export of data into .pst & .msg files.   
This consideration is further detailed here:  [Considerations](https://helpcenter.veeam.com/docs/vbo365/guide/vex_considerations.html?ver=40)


  
# Links
--------

[Veeam help center for Tenants](https://helpcenter.veeam.com/archive/vbo365/40/guide/vbo_baas_tenant.html)