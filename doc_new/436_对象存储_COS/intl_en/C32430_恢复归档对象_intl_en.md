## Overview
Archived objects can be restored in the COS Console, so that they can be accessed or manipulated. For more information about object storage classes, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).

>The restoration operation will create a replica of the object in standard storage class, which can be read and downloaded. The object replica will be billed as a standard storage object. If the source object is not deleted, it will continue to be billed as an archive storage object. For pricing details, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).


## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket name to enter the bucket details page.
![](https://main.qcloudimg.com/raw/b270a42c40ed049811168072818fba1e.png)
3. In the "File List" module on the bucket details page, click **Restore** in the "Action" column to the right of the object you want to restore.
![](https://main.qcloudimg.com/raw/d6a22d2f433ddef9a7e87c0c97b4142b.png)
4. In the dialog box for restoring the archived object, configure the restoration mode and the validity period in days of the replica. The related configuration items are detailed below.
 **Restoration Mode**: Standard, Expedited, or Batch mode.
 - Expedited mode: This is the fastest way of restoration. Files below 256 MB can be restored in 1 to 5 minutes. When you need to access the archival data urgently under certain circumstances, using this mode can greatly reduce the time required and increase the efficiency.
 - Standard mode: Restoration can be completed generally in 3 to 5 hours.
 - Batch mode: If your need for the archival data is not urgent, this mode can help retrieve massive amounts of data generally in 5 to 12 hours with the lowest cost.

 **Replica Validity Period**: Set in how many days the replica should automatically expire and be deleted. The value range is 1 to 365 days. After the object is successfully restored, you can click **Restore** again to change the validity period of the replica in the pop-up window.
 See the figure below:
![](https://main.qcloudimg.com/raw/091c8df1d6d1d33b54b59e31a74f2c02.png)

5. Click **OK** after the configuration items are set, and the object restoration will start. You can click **Details** to enter the object details page and check whether the restoration has been completed.
![](https://main.qcloudimg.com/raw/c32db86c14d8d9cbf259083bb51899c7.png)
6. After confirming that the object has been successfully restored, you can click **Restore** again to modify the validity period of its replica.
![](https://main.qcloudimg.com/raw/d406dd5f6f7b3ed504e9101b1baf192d.png)
7. Enter the object details page where you can access, download, and do more with the object.
![](https://main.qcloudimg.com/raw/2c60806f06e201c804c71af66706fa70.png)




