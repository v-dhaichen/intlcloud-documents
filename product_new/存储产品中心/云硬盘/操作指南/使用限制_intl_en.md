| Limit Type | Description |
| --- |  --- |
| Elastic cloud disk capability | Starting in May, 2018, all data disks purchased with CVMs are elastic cloud disks, which support unmounting and remounting on CVMs. This feature is supported in all [Availability Zones](https://cloud.tencent.com/document/api/213/15707). |
| Cloud disk performance limits | I/O performance is in effect concurrently. <br/>For example, a SSD with 1TB and a maximum random IOPS of up to 26,000 means that its IOPS for both reads and writes can reach this value. Meanwhile, because of multiple performance limits, if the I/O block size is 4KB/8KB in this example, I/O can reach the maximum IOPS; if its block size is 16KB, I/O cannot reach the maximum IOPS (throughput has already reached the limit of 260MB/s). |
| The number of elastic cloud disks that can be mounted on one CVM | Maximum of 20 disks. |
| Snapshot quota of a single region | 64 + the number of cloud disks in the region * 64 (units). |
| Limit on cloud disks mounted on CVMs | CVMs and cloud disks must be in the same availability zone. |
| Snapshot rollback limit | Snapshot data can only be rolled back to the source cloud disk where the snapshot was created. |
| Limit on the type of cloud disks created using snapshots | You can only use data disk snapshots to create new elastic cloud disks. |
| Limit on the size of cloud disks created using snapshots | The capacity of the new cloud disk created using snapshots must be larger than or equal to that of the snapshot source disk. |


