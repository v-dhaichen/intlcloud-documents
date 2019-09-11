﻿

COS offers three object storage classes for different object access frequencies: standard storage, standard infrequent access storage, and archive storage.

> When an object is uploaded, if the storage class is not set, it defaults to **standard storage**.

## Standard Storage

Standard storage (Standard) provides object storage services featuring high reliability, availability, and performance.

It offers low access latency and high throughput, making it suitable for business scenarios where a large number of trending files is accessed in real time with frequent data interactions.

**Features**
- High performance and availability
- Persistence: 99.999999999%
- Availability: 99.95%
- Response: Within milliseconds
- Supported regions: All
- Storage cost: Standard

**Applicable scenarios**

Trending videos, social networking photos, mobile apps, games, and dynamic websites.

## Standard Infrequent Access Storage

Standard infrequent access storage (Standard_IA) provides object storage services featuring high reliability and low storage cost and access latency.

It offers lowered pricing for storage and keeps the first-byte access time within milliseconds, ensuring that data can be retrieved quickly with no wait. However, data retrieval incurs fees. It is suitable for business scenarios with low access frequency (e.g., once or twice per month).

**Features**

- Low-frequency access, real-time response
- Persistence: 99.999999999%
- Availability: 99.9%
- Minimum billing duration: 30 days
- Minimum object size: 64 KB
- First-byte delay: Within milliseconds
- Supported regions: All
- Storage cost: Low

**Applicable scenarios**

Online file storage, big data analytics, governmental/organizational business data, low-frequency archives, and monitoring data.

## Archive Storage

Archive storage (Archive) provides object storage services featuring high reliability, extremely low storage cost, and long-term retention.

It offers the lowest unit price of storage but requires a longer unfreezing time when data is read, making it suitable for archival data that requires long-term retention.

**Features**

- High data persistence and service availability, low cost
- Data persistence: 99.999999999%
- Availability: 99.9%
- Minimum billing duration: 90 days
- Response: Prior application for data restoration required
- Supported regions: Regions in Mainland China only
- Storage cost: Very low

**Applicable scenarios**

Archive of compliance documents (e.g., archival data, medical images, and scientific materials), lifecycle files, operational logs, and remote disaster recovery.

## Comparison of Storage Types

Item 	 | Standard | 	Standard_IA | 	Archive
---|---|---|----
Data persistence |	99.999999999%	|99.999999999%|	99.999999999%
Service availability 	|99.95%	|99.9%	|99.9%
Response 	| Within milliseconds 	| Within milliseconds 	| Prior application for data restoration required
Minimum storage size for billing 	| Calculated by actual size of objects 	| 64KB 	| 48KB
Minimum billing duration 	| No limit 	| 30 days 	| 90 days
Supported regions 	| All 	| All 	| Regions in Mainland China only
Storage cost 	| Standard 	| Low 	| Very low
Data retrieval cost 	| None 	| Low 	| High
Read/write request cost 	| Very low 	| Low 	| Very low (data needs to be restored to standard storage and then will be subject to the billing rules of standard storage)
