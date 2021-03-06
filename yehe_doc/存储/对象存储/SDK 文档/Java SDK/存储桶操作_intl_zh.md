## 简介

本文档提供关于存储桶的基本操作和访问控制列表（ACL）的相关 API 概览以及 SDK 示例代码。

**基本操作**

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | 查询存储桶列表     | 查询指定账号下所有的存储桶列表     |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | 创建存储桶         | 在指定账号下创建一个存储桶         |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | 检索存储桶及其权限 | 检索存储桶是否存在且是否有权限访问 |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | 删除存储桶         | 删除指定账号下的空存储桶           |

**访问控制列表**

| API                                                          | 操作名         | 操作描述              |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置存储桶的 ACL 配置 |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询存储桶的 ACL 配置 |

## 基本操作

### 查询存储桶列表

#### 功能说明

查询指定账号下所有的存储桶列表。

#### 方法原型

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

#### 参数说明

无

#### 返回结果说明

- 成功：返回一个 所有 Bucket 类的列表，Bucket 类包含了 bucket 成员，location 等信息。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

#### 请求示例

[//]: # (.cssg-snippet-get-service)
```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### 创建存储桶

#### 功能说明

在指定账号下创建一个存储桶。同一用户账号下，可以创建多个存储桶，数量上限是200个（不区分地域），存储桶中的对象数量没有限制。创建存储桶是低频操作，一般建议在控制台创建 Bucket，在 SDK 进行 Object 的操作。

#### 方法原型

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：  Bucket 类，包含有关 Bucket 的描述（Bucket 的名称，owner 和创建日期）。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

#### 请求示例

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000"; //存储桶名称，格式：BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// 设置 bucket 的权限为 Private(私有读写), 其他可选有公有读私有写, 公有读写
createBucketRequest.setCannedAcl(CannedAccessControlList.Private);
Bucket bucketResult = cosClient.createBucket(createBucketRequest);
```

### 检索存储桶及其权限

#### 功能说明

检索存储桶是否存在且是否有权限访问。

#### 方法原型

```java
public boolean doesBucketExist(String bucketName) 
  throws CosClientException, CosServiceException;
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：存在返回 true，否则 false。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

#### 请求示例

[//]: # (.cssg-snippet-head-bucket)
```java
// bucket的命名规则为 BucketName-APPID ，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```

### 删除存储桶

#### 功能说明

删除指定账号下的空存储桶。

#### 方法原型

```java
public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket)
```java
// bucket的命名规则为 BucketName-APPID ，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucket(bucketName);
```

## 访问控制列表

### 设置存储桶 ACL

#### 功能说明

设置指定存储桶的访问权限控制列表（PUT Bucket acl）。该操作是覆盖操作，会覆盖已有的权限设置。ACL 包括预定义权限策略（CannedAccessControlList）或者自定义的权限控制（AccessControlList）。两类权限当同时设置时将忽略预定义策略，以自定义策略为主。

#### 方法原型

```java
// 方法 1 (设置自定义策略)
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// 方法 2 (设置预定义策略)
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// 方法 3 (以上两种方法的封装, 包含两种策略设置，如果同时设置以自定定义策略为主)
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest) 
  throws CosClientException, CosServiceException;
```

#### 参数说明

方法3参数同时包含1和2，因此以方法3为例进行介绍。

| 参数名称            | 描述           | 类型                |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | 权限设置请求类 | SetBucketAclRequest |

Request 成员说明：

| Request 成员 | 设置方法            | 描述                                                         | 类型                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 构造函数或 set 方法 | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String                  |
| acl          | 构造函数或 set 方法 | 自定义权限策略                                               | AccessControlList       |
| cannedAcl    | 构造函数或 set 方法 | 预定义策略如公有读、公有读写、私有读                         | CannedAccessControlList |

| 成员名         | 描述                            | 类型     |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | 包含所有要授权的信息            | 数组     |
| owner          | 表示 Object 或者 Owner 的拥有者 | Owner 类 |

Grant 类成员说明：

| 成员名     | 描述                                       | 类型       |
| ---------- | ------------------------------------------ | ---------- |
| grantee    | 被授权人的身份信息                         | Grantee    |
| permission | 被授权的权限信息（如可读，可写，可读可写） | Permission |

Owner 类成员说明：

| 成员名      | 描述                           | 类型   |
| ----------- | ------------------------------ | ------ |
| id          | 拥有者的身份信息               | String |
| displayname | 拥有者的名字（目前和 id 相同） | String |

CannedAccessControlList 表示预设的策略，针对的是所有人。是一个枚举类，枚举值如下所示：

| 枚举值          | 描述                                             |
| --------------- | ------------------------------------------------ |
| Private         | 私有读写（仅有 owner 可以读写）                  |
| PublicRead      | 公有读私有写（ owner 可以读写， 其他客户可以读） |
| PublicReadWrite | 公有读写（即所有人都可以读写）                   |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败）， 抛出异常 CosClientException 或者 CosServiceException。 详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-acl)
```java
// bucket的命名规则为 BucketName-APPID ，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";
// 设置自定义 ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/2779643970";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// 设置预定义 ACL
// 设置私有读写（默认新建的 bucket 都是私有读写）
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// 设置公有读私有写
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// 设置公有读写
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```

### 查询存储桶 ACL

#### 功能说明

查询指定存储桶的访问权限控制列表。

#### 方法原型

```java
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket 的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：返回一个 Bucket 的 ACL。 
- 失败：发生错误（如身份认证失败）， 抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-acl)
```java
// bucket的命名规则为 BucketName-APPID ，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";
AccessControlList acl = cosClient.getBucketAcl(bucketName);
```
