## Description
This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket. If the bucket does not have a lifecycle rule configured, NoSuchLifecycleConfiguration will be returned.

## Request
### Sample Request

```shell
GET /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special Headers
This request operation has no special request headers.

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
This response has no special response headers.

### Response Body
The content and meaning of each element in the response body are the same as those in the request body for PUT Bucket lifecycle. For more information, see the Request Body Node Descriptions section in [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280).

### Error Codes
There are no special error messages for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

### Request
```shell
GET /?lifecycle HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 12:23:54 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502857357;1502937357&q-key-time=1502857357;1502937357&q-header-list=host&q-url-param-list=lifecycle&q-signature=da155cda3461bee7422ee95367ac8013ef847e02

```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 312
Date: Wed, 16 Aug 2017 12:23:54 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDM5NWFfMjQ4OGY3Xzc3NGRfMjA=

<LifecycleConfiguration>
  <Rule>
    <ID>id1</ID>
    <Filter>
       <Prefix>documents/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Transition>
      <Days>100</Days>
      <StorageClass>STANDARD_IA</StorageClass>
    </Transition>
  </Rule>
  <Rule>
    <ID>id2</ID>
    <Filter>
       <Prefix>logs/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Expiration>
      <Days>10</Days>
    </Expiration>
  </Rule>
</LifecycleConfiguration>
```
