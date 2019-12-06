## Overview

Tencent Cloud Cloud Object Storage (COS) offers a service availability of 99.95% and reliability of 99.999999999%. Due to uncontrollable factors such as natural disasters and fiber-optic cable failures, neither the availability nor the reliability of in-cloud data can reach 100%; however, extremely high availability and reliability are required in certain industries like finance because of the business particularity.

In order to guarantee business continuity and stability and meet the demand for high availability and reliability, COS provides high-availability disaster recovery solutions based on cross-region replication. When using COS, you are recommended to back up data and make disaster recovery plan for your data based on your actual needs for uninterrupted and smooth business operations.

This document describes a disaster recovery solution based on cross-region replication (i.e., master/slave switch of cloud-based businesses) and a high-availability solution based on cross-region replication where high business availability is achieved with the aid of different products and features such as cross-region replication, origin-pull, SCF, and CDN.

## Backup and Disaster Recovery Solution Based on Cross-region Replication

Disaster recovery entails three elements: redundancy, remote, and replication.
- Redundancy: Data should be backed up simultaneously to another available system.
- Remote: Backup data should be stored in another remote region, as disasters often extend geographically and only a long enough distance can guarantee the availability of redundant data.
- Replication: Data loss during backup should be reduced down to zero.

The cross-region replication feature of COS enables cross-region sync of incremental data. Data uploaded by you can be copied to a bucket in another region in seconds or minutes, depending on the file size and the distance. Cross-region replication allows you to make a remote redundant backup of data for disaster recovery and business continuity. For more information, see [Cross-region Replication Overview](https://intl.cloud.tencent.com/document/product/436/19237). To enable this feature, you need to enable versioning first. For more information on versioning, see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

The schematic diagram of the backup and disaster recovery architecture based on cross-region replication is as shown below:
![](https://main.qcloudimg.com/raw/2b30c24aae10ac2cfb8e91e6330a4910.png)

Under this architecture, your bucket A and bucket B are the master and slave to each other. If your data is stored in bucket A, then bucket B in another region is the slave bucket. In order to ensure business continuity and stability, you have configured cross-region replication rules for bucket A and bucket B respectively. According to the rules, incremental data in bucket A will be automatically replicated to bucket B, and vice versa.

> After the incremental data in bucket A is replicated to bucket B, although it is "incremental" in bucket B, it will not be replicated to bucket A.

Normally, both your master read request linkage and write request linkage point to bucket A, and all incremental data will be automatically, incrementally, and synchronously replicated to bucket B as backup data. You can add a network quality detection module to the upload or download program at the business side, allowing the read and write request linkages to quickly switch to bucket B when a failure is detected in bucket A.

> Network quality detection can be implemented based on SCF. For more information.<!-- see [Scheduled Automatic Testing and Alarming via Email]()--> You can change the URLs to be automatically tested to the domain names of the master and slaver buckets by modifying the function code and change the alarming code snippets to other measures required by your business.

## High-availability Solution Based on Cross-region Replication

The section above describes a backup and disaster recovery solution based on cross-region replication, which uses existing Tencent Cloud products and features to achieve data backup and disaster recovery switch. However, real businesses may be run in complex, ever-changing environments, and the aforementioned solution may not be able to guarantee high business availability. Therefore, this section proposes a high-availability solution based on cross-region replication where high business availability is achieved with the aid of different products and features such as cross-region replication, origin-pull, SCF, and CDN.

The schematic diagram of the high business availability architecture based on cross-region replication is as shown below:
![](https://main.qcloudimg.com/raw/e56c3707f14b2e30c216e22c4c68eda0.png)

This architecture consists of the following layers:

- **High availability layer**: This layer integrates network detection and service scheduling and switches the linkage based on metrics such as linkage connectivity, which can be implemented with the aid of SCF (as described in the previous section) or on the client side according to your business needs.
- **Storage layer**: This layer typically consists of COS buckets in different regions. You can also **introduce buckets on external origin servers or in other clouds** by [setting origin-pull policies](https://intl.cloud.tencent.com/document/product/436/31508) so as to further guarantee data consistency.
- **CDN layer**: This layer provides local access through the massive amounts of edge servers of Tencent Cloud CDN, eliminating end users' need to directly access the data on your origin servers and thus ensuring data security.

The way how this architecture guarantees high business availability is as described below:

1. Normally, your master write request linkage points to bucket A, and all incremental data will be automatically and synchronously replicated to bucket B as backup data.
2. When the linkage to master bucket A fails (for example, the quality of automated testing declines or an upload fails), the client can switch the write request linkage to master bucket B, and in this case, all incremental data will also be automatically and synchronously replicated to bucket A.
3. You can also choose to make a redundant backup of your data on an external origin server or in another cloud first and then configure an origin-pull policy for bucket B. If, in extreme cases, both the linkages to master buckets A and B fail, bucket B can pull data from the origin server when the attempt to upload data to bucket B fails.

> 
> - As full redundant backups are costly, you can choose to make redundant backups of hot data (such as files uploaded in just a few hours) so as to reduce data storage costs.
>- If you choose an origin server as part of the high availability architecture, please be sure to assess the bandwidth of the origin server and the possible impact of the limit on it when designing the architecture.

4. You can read data from your bucket by directly accessing it or by [binding a CDN-accelerated domain name](https://intl.cloud.tencent.com/document/product/436/18670) to your bucket and enabling local access for end users through the edge servers of Tencent Cloud CDN. If your business data involves content delivery, or you don't want your end users to directly access your bucket, you are recommended to use [Tencent Cloud CDN](https://intl.cloud.tencent.com/document/product/228).

> 
> - If you want to read data from your bucket directly, your client should be able to follow 302 redirects in the HTTP protocol.
> - Tencent Cloud CDN boasts nearly a thousand edge servers which provide adjacent access nodes to increase the data read speed. You can bind multiple origin servers to CDN as master and slave servers in order to ensure high availability. For more information, see [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289).
> - If you want to secure your origin servers as much as possible, you can set private-read/write permission for them and enable CDN origin-pull authentication so as to allow your end users to anonymously access the data cached on the CDN edge servers whiling protecting the security of the data on the origin servers.

## Reference Documents

The following documents can help you easily implement the high-availability disaster recovery architecture:

- [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883)
- [Cross-region Replication Overview](https://intl.cloud.tencent.com/document/product/436/19237)<!-- - [Scheduled Automated Testing and Alarming via Email]()-->
- [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508)
- [CDN Acceleration Configuration](https://intl.cloud.tencent.com/document/product/436/18670)
- [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289)
- [Domain Name Connection](https://intl.cloud.tencent.com/document/product/228/5734)
