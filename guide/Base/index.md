---
title: Starting point
has_children: true
nav_order: 200
has_toc: false
---

# Staring Point

This section covers topics which are relevant when building the designed solution and configuring
Veeam Backup for Microsoft Office 365 infrastructure components, such as proxies and repositories.

For general information about these topics please check the
[Deployment](https://helpcenter.veeam.com/docs/vbo365/guide/vbo_deployment.html) and read about the
specific components in the
[Backup Infrastructure](https://helpcenter.veeam.com/docs/vbo365/guide/backup_infrastructure.html)
section.

## Antivirus Software Exceptions for Veeam Processes

Configure antivirus exceptions as described in [Veeam KB3074] to avoid performance issues. This is
true for all servers within a Veeam Backup for Microsoft Office 365 deployment.

When experiencing resource bottlenecks a reason can be the installed antivirus software. Depending
on the software it can compete on CPU time and add latency to I/O operations for scanning these.
By putting the VBO processes to the exclusion list of the anti-virus software, this effect can be
mitigated. As this incurrs punching a hole in the systems security this should be handled with care.

We also found Windows Defender Antimalware Service Executable to take a lot of resources on VBO
proxies. This can be avoided by excluding the executable from Windows Defender itself. See this
[Emisoft Blogpost] for details on how to configure this.

## Resources

- [Veeam KB3074] - Details on antivirus exclusions for VBO
- [Emisoft Blogpost] - How to fix ‘Antimalware Service Executable’ high CPU usage
- [VBO-AddDefenderExclusions] - PowerShell script to automatically configure exclusions in Windows
  Defender based on KB3074

[veeam kb3074]: https://www.veeam.com/kb3074
[emisoft blogpost]: https://blog.emsisoft.com/en/28620/antimalware-service-executable/
[VBO-AddDefenderExclusions]: https://github.com/VeeamHub/powershell/tree/master/VBO-AddDefenderExclusions
