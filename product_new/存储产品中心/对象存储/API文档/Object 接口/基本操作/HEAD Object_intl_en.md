## Description

This API (HEAD Object) is used to determine whether the specified object exists and you have permission to access it and to get its metadata if it is accessible. The requester of this API should have the permission to read the target object, or the target object should be public-read.

#### Versioning

If versioning is enabled, the HEAD operation will return the latest version of the metadata. To return a previous version of the metadata, use the versionId request parameter.

## Request

#### Sample Request

```shell
HEAD /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

| Name | Description | Type | Required |
| --------- | ------------------------- | ------ | -------- |
| versionId | Specifies the version ID of the object to be queried | string | No |

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information on the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------ | -------- |
| If-Modified-Since | If the object is modified after the specified time, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | string | No |
| If-Unmodified-Since | If the object is not modified after the specified time, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned | string | No |
| If-Match | If the ETag of the object is the same as the specified value, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 412 (Precondition Failed) will be returned | string | No |
| If-None-Match | If the ETag of the object is different from the specified value, HTTP status code 200 (OK) will be returned; otherwise, HTTP status code 304 (Not Modified) will be returned | string | No |

**Server-side encryption-related headers**

If server-side encryption is used for the specified object and the encryption method is SSE-C, the headers related to server-side encryption needs to be specified for decrypting the object. For more information. see [Server-side Encryption-specific Headers](https://intl.cloud.tencent.com/document/product/436/7728#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Request Body

This API has no request body.

## Response

#### Response Header

In addition to common response headers, this API returns the following response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| Cache-Control | Cache policy as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Content-Disposition | Filename as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| Expires | Cache expiration time as defined in RFC 2616, which will be returned only if it is contained in the object metadata | string |
| x-cos-meta-\* | This includes the suffix and information of the user-defined metadata header | string |
| x-cos-storage-class | Object storage class, such as STANDARD_IA and ARCHIVE. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). This header will be returned only if the object is not in STANDARD storage class | Enum |

**Versioning-related headers**

For versioned objects, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Server-side encryption-related headers**

If server-side encryption is used for the specified object, this API will return the server-side encryption-specific headers. For more information. see [Server-side Encryption-specific Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API is empty.

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```shell
HEAD /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 09 Aug 2019 10:21:01 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565346061;1565353261&q-key-time=1565346061;1565353261&q-header-list=date;host&q-url-param-list=&q-signature=82f401cf54cd6ad0331d1c0b8c827bf8f2f9****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 13
Connection: close
Date: Fri, 09 Aug 2019 10:21:01 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Fri, 09 Aug 2019 10:20:56 GMT
Server: tencent-cos
x-cos-request-id: NWQ0ZDQ5MGRfNmRjMDJhMDlfOThjMl8xNzE2****
```
