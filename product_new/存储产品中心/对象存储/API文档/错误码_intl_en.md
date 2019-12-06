## Overview

This document describes the error codes and corresponding error messages returned when a request fails.

## Error Response

Content-Type: application/xml

Corresponding HTTP status code: 3XX, 4XX, and 5XX. In particular, for the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) API, even if the HTTP status code is 200, an error may still be included in the response body.

#### Response Body

```xml
<?xml version='1.0' encoding='utf-8' ?>
<Error>
	<Code>string</Code>
	<Message>string</Message>
	<Resource>string</Resource>
	<RequestId>string</RequestId>
	<TraceId>string</TraceId>
</Error>
```

The detailed nodes are described as follows:

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Error| No | Contains all error information |Container

**Content of the Container node Error :**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Code|Error| Error code used to locate the unique error condition and determine the error scenario. See below for specific error codes | string
Message|Error| Specific error message |string
Resource|Error| Requested resource: bucket address or object address |string
RequestId|Error| Whenever a request is sent, the server will automatically generate an ID for it, which can help locate problems faster |string
TraceId|Error| Whenever an error occurs, the server will automatically generate an ID for it, which can help locate problems faster |string

## Error Code List

**3XX errors**

| Error Code | Description | HTTP Status Code |
| ----------------- | ------------------------------------------------------------ | --------------------- |
| PermanentRedirect | This resource has been permanently relocated. Please use the HTTP Location response header to redirect to the correct location | 301 Moved Permanently |
| TemporaryRedirect | This resource has been temporarily relocated. Please use the HTTP Location response header to redirect to the correct location | 302 Moved Temporarily |
| Redirect | Temporarily redirected | 307 Moved Temporarily |
| TemporaryRedirect | You will be temporarily redirected during the DNS update | 307 Moved Temporarily |

**4XX errors**

| Error Code | Description | HTTP Status Code |
| ----------------------------------- | ------------------------------------------------------------ | ----------------------------------- |
| AppendPositionErr | The object length doesn't match the position during the Append operation | 400 Bad Request |
| AttachmentFull | The maximum number of ACLs and policies is reached | 400 Bad Request |
| BadDigest | The provided Content-MD5 value is different from the MD5 hash of the request body received by the server | 400 Bad Request |
| EntityTooLarge | The size of the uploaded object exceeds the specified maximum value | 400 Bad Request |
| EntityTooSmall | The size of the uploaded object is below the specified minimum value. This error generally occurs in multipart uploads | 400 Bad Request |
| IncorrectNumberOfFilesInPostRequest | Only one object can be uploaded in one POST request | 400 Bad Request |
| InvalidArgument | Invalid request parameter | 400 Bad Request |
| InvalidBucketName | Invalid bucket name | 400 Bad Request |
| InvalidCopySource | Invalid source for object copy | 400 Bad Request |
| InvalidDigest | The given Content-MD5 value is invalid | 400 Bad Request |
| InvalidPart | Missing part | 400 Bad Request |
| InvalidPartOrder | Part numbers are not continuous | 400 Bad Request |
| InvalidRegionName | Invalid region name | 400 Bad Request |
| InvalidRequest | Invalid request | 400 Bad Request |
| InvalidSHA1Digest | Invalid SHA1 verification of the request content | 400 Bad Request |
| InvalidURI | Invalid URI | 400 Bad Request |
| KeyTooLong | The object key is too long | 400 Bad Request |
| LifeCycleIdNotUnique | The lifecycle ID is not unique | 400 Bad Request |
| LifeCycleRuleConflicted | There is a conflict in the lifecycle settings | 400 Bad Request |
| MalformedPOSTRequest | The request body content of this POST request is invalid | 400 Bad Request |
| MalformedXML | The XML format of the request body does not conform to the XML syntax | 400 Bad Request |
| MissingAppid | APPID is missing in the request header | 400 Bad Request |
| MissingContentMD5 | Content-MD5 is missing in the request header | 400 Bad Request |
| MissingHost | Host is missing in the request header | 400 Bad Request |
| MissingRequestBodyError | Missing request body | 400 Bad Request |
| MultiBucketNotSupport | Only one destination bucket can be set for cross-region replication | 400 Bad Request |
| NoSuchVersion | The specified version does not exist | 400 Bad Request |
| NotSupportedStorageClass | The specified storage class is not supported | 400 Bad Request |
| ObjectNotAppendable | The specified object cannot be appended | 400 Bad Request |
| PolicyFull | The maximum number of ACLs and policies is reached | 400 Bad Request |
| RequestTimeOut | Data read timed out. Check your network speed or reduce the number of concurrent uploads | 400 Bad Request |
| TooManyBuckets | The maximum number of buckets (200) has been reached | 400 Bad Request |
| UnexpectedContent | The request does not support the relevant content | 400 Bad Request |
| VerifyAlgorithmNotSupported | The verification algorithm is not supported | 400 Bad Request |
| WebsiteURLInvalid | Invalid custom domain name URL | 400 Bad Request |
| XMLSizeLimit                        | The length of XML has exceeded the limit                                             | 400 Bad Request                     |
| AccessDenied | Access denied due to wrong signature or permission | 403 Forbidden |
| ExpiredToken | The signature string has expired | 403 Forbidden |
| InvalidAccessKeyId | The SecretID does not exist | 403 Forbidden |
| InvalidObjectState | The request content conflicts with the object attributes | 403 Forbidden |
| InvalidObjectStorage | Invalid storage class | 403 Forbidden |
| RequestTimeTooSkewed | The local time is over 15 minutes different from the server time | 403 Forbidden |
| SignatureDoesNotMatch | The signature calculated by the client does not match that calculated by the COS server | 403 Forbidden |
| NoSuchBucket | The specified bucket does not exist | 404 Not Found |
| NoSuchCopySource | The object copy source does not exist | 404 Not Found |
| NoSuchCORSConfiguration | The specified CORS configuration does not exist | 404 Not Found |
| NoSuchKey | The specified object key does not exist | 404 Not Found |
| NoSuchLifecycleConfiguration | The specified lifecycle configuration does not exist | 404 Not Found |
| NoSuchTagSet | The specified tag set does not exist | 404 Not Found |
| NoSuchUpload | The UploadId specified for the multipart upload does not exist | 404 Not Found |
| NoSuchWebsiteConfiguration | The static website configuration does not exist | 404 Not Found |
| MethodNotAllowed | This resource does not support this HTTP method | 405 Method Not Allowed |
| RestoreNonArchiveObject | It is not allowed to restored a non-archived object | 405 Method Not Allowed |
| BucketAlreadyExists | The specified bucket already exists. | 409 Conflict |
| BucketAlreadyOwnedByYou | The specified bucket already exists and was created by the current account. | 409 Conflict |
| BucketNotEmpty | The bucket is not empty | 409 Conflict |
| InvalidBucketState | The bucket status conflicts with the operation request; for example, versioning management conflicts with cross-region replication | 409 Conflict |
| PathConflict | Millisecond-level concurrence conflict occurred for objects with the same name | 409 Conflict |
| RestoreAlreadyInProgress | This object is being restored | 409 Conflict |
| MissingContentLength | The Content-Length request header is missing | 411 Length Required |
| PreconditionFailed | Precondition match failed | 412 Precondition |
| InvalidRange | The requested object range is invalid | 416 Requested Range Not Satisfiable |
| UnavailableForLegalReasons | Unavailable for legal reasons | 451 Unavailable For Legal Reasons |

**5XX errors**

| Error Code | Description | HTTP Status Code |
| ------------------ | -------------------------- | ----------------------- |
| InternalErrror | Internal server error | 500 Internal Server |
| NotImplemented | The request has not been implemented yet | 501 Not Implemented |
| ServiceUnavailable | The service is temporarily unavailable. Please try again | 503 Service Unavailable |
| SlowDown | Please reduce the frequency of access | 503 Slow Down |
