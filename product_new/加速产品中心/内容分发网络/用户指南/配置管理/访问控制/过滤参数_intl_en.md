CDN provides an Ignore Query String switch, which allows you to control whether to filter the parameters after **"?"** in user requests’ URLs during caching. You can use this feature for flexible version control or token-based authentication.
> If different parameters in your resource URL represent the same content, we recommended you enable the ignore query string feature to effectively improve the cache hit rate.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/90529e7508d4a9d8166b34ff4f1aa37c.png)
2. Click the **Access Control** tab and configure the ignore query string feature in the "Ignore Query String" module.
![img](https://main.qcloudimg.com/raw/c62b2afcd3702542677772a7872bd0e2.png)

> If your accelerated business type is download or video on-demand, the ignore query string feature is enabled by default. If the accelerated type is static content, it is disabled by default.

## Sample Case
When CDN caches resources on the node storage structure, it uses cache_key as an index to search for stored resources.
1. If the configuration is as follows:
   ![img](https://main.qcloudimg.com/raw/9fafd815873f3f3b13ba9d17124efcca.png)
   - User A requests a resource with URL `http://www.test.com/1.jpg?version=1.1`. When a node stores the resource, the corresponding `cache_key` is `www.test.com/1.jpg. ` with the parameters after "?" ignored.
   - User B requests a resource with URL `http://www.test.com/1.jpg?version=1.2`, which will also be looked up with `cache_key` as `www.test.com/1.jpg`, so the content can be directly hit because it is the same as that requested by user A.
2. If the configuration is as follows:
   ![img](https://main.qcloudimg.com/raw/045c3b7269034dde91359deea66433d3.png)
   - User A requests a resource with URL `http://www.test.com/1.jpg?version=1.1`. When a node stores the resource, the corresponding `cache_key` is `www.test.com/1.jpg?version=1.1` with the parameters after "?" not ignored.
   - User B requests a resource with URL `http://www.test.com/1.jpg?version=1.2`, which will be looked up with `cache_key` as `www.test.com/1.jpg?version=1.2`. Because there is no hit, the corresponding content will be obtained from the origin server again for caching.
