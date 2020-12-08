---
title: VBO Server
parent: Build & Configure
nav_order: 100
has_children: true
has_toc: false
---
# Veeam Backup for Microsoft Office 365 Server

The Veeam Backup for Microsoft Office 365 server role hosts the product's management console and manages the attached proxies and repositories.

## Same OS on VBO management and proxy/repo servers
Run the **same OS version as on proxy and repository servers** to reduce compatibility issues and 
reduce support effort.

VBO leverages the Microsoft Jet Blue database which is built into the Microsoft operating system. As 
every OS version brings another built-in version of the Jet Blue database engine it is recommended 
to use the same OS version on all VBO infrastructure components to avoid incompatibility issues.

Also drilling down problems is much easier when all components run on the same operating system and
have the same feature level, security settings and quirks.

## Resources
- [Veeam HelpCenter - Veeam Backup for Microsoft Office 365 User Guide](https://helpcenter.veeam.com/docs/vbo365/guide/)
    - [System Requirements](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_system_requirements.html)
    - [Installing Veeam Backup for Microsoft Office 365](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_installing_vbo.html)
    - [General Application Settings](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_general_application_settings.html)
