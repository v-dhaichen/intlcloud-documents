## Description
This API (Upload Part) is used to upload an object to COS in parts. It supports up to 10,000 parts of 1 MB to 5 GB each in size, and the last part can be less than 1 MB.

### Detail Analysis
1. To upload an object in parts, you need to use the Initiate Multipart Upload API to initialize a multipart upload. After initialization, an uploadId will be returned, which uniquely identifies this upload.
2. Every time you request the Upload Part API, you need to pass in the partNumber (which is the part number) and uploadId parameters. Out-of-order uploading is supported.
3. When the uploadId and partNumber of a newly uploaded part are the same as those of a previously uploaded part, the former will overwrite the latter. A 404 NoSuchUpload error will be returned if the uploadId does not exist.

## Request
### Sample Request

```shell
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: Size
Authorization: Auth String

[Object]
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
**Required headers**
The following required request headers are needed for the implementation of this request operation as detailed below:

| Name | Description | Type | Required |
| :------------- | :---------------------------- | :----- | :--- |
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | String | Yes |

**Recommended headers**
The following request headers are recommended for the implementation of this request operation as detailed below:

| Name | Description | Type | Required |
| :---------- | :--------------------------------------- | :----- | :--- |
| Expect | HTTP request length in bytes as defined in RFC 2616 | String | No |
| Content-MD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed | String | No |

#### Request Parameters
See the details below:

| Parameter Name | Description | Type | Required |
| :--------- | :--------------------------------------- | :----- | :--- |
| partNumber  | Identifies a part number                                       | String | Yes  |
| uploadId | ID of this multipart upload. <br>When the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | String | Yes |

### Request Body
The request body of this request is the data content of the part.

## Response

### Response Headers
#### Common Response Headers 
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response may contain the following response headers:

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | If it is specified to use server-side encryption when the file is uploaded, this response header will be returned. Enumerated value: AES256 | String |
|x-cos-storage-class| Storage class information of the object. COS will return this response header for all objects except those in the STANDARD storage class. Enumerated values: STANDARD_IA, ARCHIVE| String |

### Response Body
The response body of this request is empty.

### Error Codes
There are no special error messages for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

### Request
```shell
PUT /exampleobject?partNumber=1&uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727403;32557623403&q-key-time=1484727403;32557623403&q-header-list=host&q-url-param-list=partNumber;uploadId&q-signature=bfc54518ca8fc31b3ea287f1ed2a0dd8c8e88a1d
Content-Length: 10485760

[Object]
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Etag: "e1e5b4965bc7d30880ed6d226f78a5390f1c09fc"
Server: tencent-cos
x-cos-request-id: NTg3ZjI0NzlfOWIxZjRlXzZmNGJfMWYy
```
