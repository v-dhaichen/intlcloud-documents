## Description

This document describes the common response headers that will be used by APIs. The headers mentioned below will not be detailed again in specific API documents.

## Response Headers

<table>
   <tr>
      <th>Header Name</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Length</td>
      <td>HTTP response length in bytes as defined in RFC 2616</td>
      <td>string</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>HTTP response content type (MIME) as defined in RFC 2616.</td>
      <td>string</td>
   </tr>
   <tr>
      <td>Connection</td>
      <td>Indicates whether the network connection will be closed after the response is completed as defined in RFC 2616. Enumerated values: keep-alive, close. </td>
      <td>Enum</td>
   </tr>
   <tr>
      <td>Date</td>
			<td>Server response time in GMT format as defined in RFC 1123, such as <code>Wed, 29 May 2019 04:10:12 GMT</code>. </td>
      <td>string</td>
   </tr>
   <tr>
      <td>Etag</td>
      <td>An entity tag (ETag) is an information tag that identifies the content of an object when it is created, such as<code>"8e0b617ca298a564c3331da28dcb50df"</code>. It can be used to check whether the content of the object has changed. This header does not necessarily return the MD5 checksum value of the object; instead, it may vary depending on how the object is uploaded and encrypted. </td>
      <td>string</td>
   </tr>
   <tr>
      <td>Server</td>
			<td>Name of the server that accepts the request and returns the response. Default value: <code>tencent-cos</code>. </td>
      <td>string</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-request-id</td>
      <td>Every time a request is sent, the server will automatically generate a unique ID for it.</td>
      <td>string</td>
   </tr>
   <tr>
      <td>x-cos-trace-id</td>
      <td>Whenever an error occurs with a request, the server will automatically generate an ID for the error. This header will be included in the response only if the request goes wrong. </td>
      <td>string</td>
   </tr>
</table>


## Server-side Encryption Headers

For APIs that support server-side encryption (SSE) and use SSE in the request, the following response headers will be returned according to the specific encryption method. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

### SSE-COS

<table>
   <tr>
      <th>Header Name</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-server-side-encryption</td>
      <td>If an object is uploaded with SSE-COS or an SSE-COS-encrypted object is downloaded, the response of the request will return this header, indicating the server-side encryption algorithm used when the object is uploaded. </td>
      <td>string</td>
   </tr>
</table>

### SSE-C

| Header Name | Description | Type  |
| ------------------ | ---------------------------------------- | ------ |
| x-cos-server-side-encryption-customer-algorithm | If an object is uploaded with SSE-C or an SSE-C-encrypted object is downloaded, the response of the request will return this header, indicating the server-side encryption algorithm used when the object is uploaded. | string |
| x-cos-server-side-encryption-customer-key-MD5   | Base64-encoded MD5 hash of the server-side encryption key used during object upload, <br>such as `U5L61r7jcwdNvT7frmUG8g==` | string |
