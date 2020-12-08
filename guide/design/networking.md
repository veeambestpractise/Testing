---
title: Networking
parent: Design
nav_order: 600
---
# Networking

## Best Practice

* Static IPv4 for VBO server
* Static IPv4 for VBO proxy/repo server
* Create A and PTR records in DNS
* Prefer IPv4 over IPv6
* VBO server and proxies need to be part of the same (or trusted) Active Directory domain

## Explanation

Working stable communication between the components with working DNS name resolution is key to prevent hard to trace errors.
