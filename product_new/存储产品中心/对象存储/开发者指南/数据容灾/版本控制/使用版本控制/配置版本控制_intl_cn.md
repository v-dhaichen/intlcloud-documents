## 使用场景
利用版本控制功能，您可以在存储桶中存放对象的多个版本，并且实现检索、删除和还原指定版本对象。
了解版本控制详情信息，请参见 [版本控制概述](https://intl.cloud.tencent.com/document/product/436/19883) 文档。

>!只有主账号和被授权的子账号可以配置存储桶的版本控制状态。

## 使用方法

### 使用对象存储控制台
您可以使用对象存储控制台开启版本控制功能，详情请参见 [设置版本控制](https://cloud.tencent.com/document/product/436/19881) 控制台指南文档。

### 使用 REST API

您可以直接使用 REST API 配置存储桶的版本控制和管理版本控制状态下存储桶中的对象，请参考以下 API 文档部分：
- [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889)
- [GET Buket versioning](https://intl.cloud.tencent.com/document/product/436/19888)
- [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
- [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### 使用 SDK

您可以直接调用 SDK 的版本控制方法，详情请参见下列各语言 SDK 文档：

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
