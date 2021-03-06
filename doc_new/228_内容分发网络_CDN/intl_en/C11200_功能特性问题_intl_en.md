### Does Tencent Cloud CDN have the acceleration capability on a global scale?
Yes. Tencent Cloud CDN has opened access to over 100 cache nodes accumulated over the past decade, across more than 30 countries and regions, providing customers with the acceleration capabilities on a global scale.

### Do changes need to be made to origin server for the acceleration service to apply after the connection to CDN?
Basically, no change is needed. However, in order to achieve a better acceleration result, we recommend that you assign static and dynamic files to different domain names and only accelerate the static resources.

### Does Tencent Cloud CDN support cross-region access?
Yes. No restriction is imposed on cross-region access in Tencent Cloud CDN. If cross-region access is needed for your website, you simply need to configure the Access-Control-Allow-Origin field in your website, or configure cross-region headers for your domain name in the CDN. For more information, see [HTTP Header Configuration](https://cloud.tencent.com/doc/product/228/6296).

### Where can I download the CDN access log?
You can download the CDN access log in the CDN Console. For more information, see [Download Log](https://cloud.tencent.com/document/product/228/6316#.E6.97.A5.E5.BF.97.E4.B8.8B.E8.BD.BD).

### How do I use the Fault Self-diagnosis tool?
You can use the Fault Self-diagnosis tool to test DNS resolution, link quality, site availability and data access consistency for the accessed domain names. For more information, see [Fault Self-diagnosis](https://cloud.tencent.com/document/product/228/6304). This tool is subject to the configuration of your local network environment and cannot fully represent the results of internet-wide testing.

### What is the difference between the local access diagnostics and the user access diagnostics?
Local Access Diagnostics: When you find an error with one of your resource accesses, you can initiate a test with the Local Access Diagnostics.
User Access Diagnostics: When your users report an error with resource access, you can pinpoint the problem through "User Access Diagnostics" and solve the problem by performing the actions suggested by Tencent Cloud.

### Does CDN support POST requests?
Yes. CDN supports POST requests.

### Does CDN support the origin server's Cache-Control setting?
By default, Tencent Cloud CDN supports origin server's Cache-Control setting.

### Does CDN support GZIP compression?
CDN compresses the files with a size between 256 Byte and 2048 KB and a filename extension of .js, .html, .css, .xml, .json, .shtml, and .htm to Gzip files to help you reduce your traffic.

### Does CDN support ports other than 80 for acceleration?
CDN accelerator supports ports 80, 443 and 8080.

### What is a CDN intermediate server?
CDN intermediate server is an intermediate-layer origin-pull server located between the customer server and CDN node. The intermediate server converges the node's origin-pull requests to reduce the origin-pull pressure on your origin server.

### How do I obtain the real client IP?
You can do so by configuring the x-forward-for header. Please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
