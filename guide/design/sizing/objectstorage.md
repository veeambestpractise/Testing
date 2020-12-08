---
title: Object Storage
parent: Sizing
grand_parent: Design
nav_order: 200
has_toc: false
---

# Object Storage

There are some special considerations when using an object storage repository
regarding sizing.

## Local Cache

As a rule of thumb provide ~1% of the source data size as local cache for
metadata for the object storage repository.

By using ~1% of the source data size as local cache on local disks on the
working repository server we can avoid ~90% of the otherwise required API calls
to the object storage in case of restores. Especially in public cloud
deployments API calls to the object storage are time sensitive (latency for the
round trip) and can cost money (charges for API calls).

Depending on the structure and type of data, the local cache size can vary (%
values are from the source data).

| Item                                      | Exchange Data | SharePoint Data |
| ----------------------------------------- | :-----------: | :-------------: |
| Average local cache size (Veeam QC tests) |   0.2% - 1%   |    0.4% - 1%    |
| Highest local cache size (Veeam QC tests) |      2%       |       6%        |

## Object Storage Data Size

Because VBO compresses the source data before putting it in object storage in
general the required space in object storage will be only ~50% of the source
data.

Compression of course depends heavily on the type and structure of source data
and can vary.

| Item                                          | Exchange Data | SharePoint |
| --------------------------------------------- | :-----------: | :--------: |
| Average size of backup data in object storage |   40% - 50%   | 45% - 55%  |

### Object Sizes

VBO does store data items in chunks to the object storage repository. These
junks are _before compression_ 5MB for Exchange data and 8MB for SharePoint and
OneDrive data.

Additionally VBO stores meta-data in own objects. These objects are small in
size (100KB or less) and can make up for up to 50% of the overall number of
objects in an object storage repository.

## API Call Cost Estimation

Normally public cloud providers will charge for API calls to the object storage.
To help calculating the costs for these API calls, see the following data from
Veeam internal tests running VBO in Azure and backing up to Azure Blob storage.

Azure Blob API calls are charged per 10,000 calls, differ per type of call
(write/read/list...) and on the Blob storage type (hot/cold...)

Please note that this data can vary based on the type and structure of the
source data. It is only intended to get a vague idea of pricing.

### Backup

#### API Calls

Average number of requests **per 100GB of backup data**.

| Backup Requests          | Exchange Data |      % | SharePoint Data |      % |
| ------------------------ | ------------: | -----: | --------------: | -----: |
| PutBlob                  |        28,981 | 91.02% |          35,268 | 81.32% |
| GetBlob                  |           308 |  0.97% |             442 |  1.02% |
| ListBlobs/ListContainers |            11 |  0.03% |             216 |  0.50% |
| DeleteBlob               |         2,527 |  7.94% |           7,156 | 16.50% |
| Other                    |            13 |  0.04% |             286 |  0.66% |
| Total                    |        32,158 |   100% |          43,802 |   100% |

#### Cost Estimation

Average backup API calls cost **per 100GB** of backup data to Azure Blob storage
(pricing December 2019):

| Azure Blob Storage              | Exchange Data | SharePoint Data |
| ------------------------------- | ------------: | --------------: |
| Azure Cool LRS[^1] (US Central) |       \$0.290 |         \$0.354 |
| Azure Cool GRS[^2] (US Central) |       \$0.580 |         \$0.708 |
| Azure Hot LRS[^1] (US Central)  |       \$0.157 |         \$0.192 |

### Synchronization

[Synchronizing repositories](https://helpcenter.veeam.com/docs/vbo365/guide/synch_tiers.html)
is required when the local cache and object storage metadata information differ.

#### API Calls

Average number of requests **per 100GB of backup data**.

| Synchronization Requests | Exchange Data |    % | SharePoint Data |    % |
| ------------------------ | ------------: | ---: | --------------: | ---: |
| PutBlob                  |         1,942 |  34% |           2,598 |  33% |
| GetBlob                  |           455 |   8% |             582 |   7% |
| ListBlobs/ListContainers |         2,929 |  51% |           4,094 |  51% |
| Other                    |           432 |   7% |             701 |   9% |
| Total                    |         5,758 | 100% |           7,975 | 100% |

#### Cost Estimation

Average synchronization API calls cost **per 100GB** of backup data in Azure
Blob storage (pricing December 2019):

| Azure Blob Storage              | Exchange Data | SharePoint Data |
| ------------------------------- | ------------: | --------------: |
| Azure Cool LRS[^1] (US Central) |       \$0.021 |         \$0.029 |
| Azure Cool GRS[^2] (US Central) |       \$0.040 |         \$0.055 |
| Azure Hot LRS[^1] (US Central)  |       \$0.019 |         \$0.027 |

[^1]: Local Redundant Storage
[^2]: Geo Redundant Storage

### Restores

The available numbers for restores are less detailed but can give you an
indication.

| Restore      |                  Exchange |             SharePoint |
| ------------ | ------------------------: | ---------------------: |
| Data         | 10.6 GB<br/> 70,061 items | 10.1 GB<br/> 529 items |
| Egress       |                   4.8 GiB |                4.7 GiB |
| Transactions |                     3,700 |                  2,840 |
