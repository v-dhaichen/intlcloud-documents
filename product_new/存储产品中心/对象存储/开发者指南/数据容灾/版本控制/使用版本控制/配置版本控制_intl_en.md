## Use Cases
By enabling versioning, you can store multiple versions of an object in a bucket and retrieve, delete, or restore a specified version.
For more information, see [Versioning Overview](https://cloud.tencent.com/document/product/436/19883).

>Only the root account and authorized sub-accounts can configure the versioning state of a bucket.

## Directions
### Configuring via the COS Console
You can refer to [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881) to learn how to encrypt objects in the console.

### Configuring via REST API

You can use the REST API to configure versioning and manage objects in buckets with different versioning states. For more information, see the following API documentation:
- [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889)
- [GET Buket versioning](https://intl.cloud.tencent.com/document/product/436/19888)
- [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
- [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### Configuring with SDK

You can directly call the Versioning method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31515#versioning)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#versioning)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523#versioning)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30597#versioning)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527#versioning)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31531#versioning)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31535#versioning)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31539#versioning)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31543#versioning)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547#versioning)
