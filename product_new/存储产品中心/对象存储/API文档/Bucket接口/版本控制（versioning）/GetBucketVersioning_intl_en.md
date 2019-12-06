## Description
The GET Bucket versioning API is used to get the versioning information of a bucket.
### Notes
1. To get the versioning state of a bucket, you need to have the permission to read the bucket.
2. There are three versioning states: not enabled, enabled, or suspended.
- If you have never enabled or suspended versioning for the bucket, the response is:
```shell
<VersioningConfiguration/>
```

- If you have enabled versioning for the bucket, the response is:
```shell
<VersioningConfiguration>
    <Status>Enabled</Status>
</VersioningConfiguration>
```
- If you have suspended versioning for the bucket, the response is:
```shell
<VersioningConfiguration>
    <Status>Suspended</Status>
</VersioningConfiguration>
```


## Request
### Sample Request

```shell
GET /?versioning HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Headers

#### Common Headers
The implementation of this request uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request does not use any special request header.

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers 
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response does not have special response headers.

### Response Body

```shell
<VersioningConfiguration>
    <Status></Status>
</VersioningConfiguration>
```

Please find the details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| --------------------------------------- | --------------------- | --------- | ------- |
| VersioningConfiguration | None | Describes the detailed information on versioning | Container |
| Status | VersioningConfiguration | Indicates whether versioning is enabled; enumerators: Suspended, Enabled | Enum |


## Samples
```shell
GET /?versioning HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9Sm****&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versioning&q-header-list=host&q-signature=5118a936049f9d44482bbb61309235cf4abe****
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 120
Connection: keep-alive
Date: Wed, 23 Aug 2017 08:15:16 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5OTRfZDNhZDM1MGFfMjYyMTFfZmU3****

<?xml version='1.0' encoding='utf-8' ?>
<VersioningConfiguration>
    <Status>Enabled</Status>
</VersioningConfiguration>
```

