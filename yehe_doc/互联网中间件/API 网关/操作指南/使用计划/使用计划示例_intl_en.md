## Operation Scenarios
To successfully call a service after it is published, you need to create a key pair and a usage plan and bind them to the service environment.
This document describes how to configure a user-specific usage plan and make it available to the users.

## Prerequisites
1. You have [created a service](https://intl.cloud.tencent.com/document/product/628/11787) and [created and debugged an API](https://intl.cloud.tencent.com/document/product/628/11795) to ensure that the API is valid and responsive.
2. You have [published a service](https://intl.cloud.tencent.com/document/product/628/11809) to a certain environment, such as the release environment.

## Directions
### Creating key pair
1. Log in to the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index) and click **Key** on the left sidebar to enter the key management page.
2. Click **Create** in the top-left corner and enter a key name in the pop-up dialog box.
Key name: up to 50 letters, digits, and underscores.
3. Click **Submit** and the system will automatically generate a key pair (`SecretId` and `SecretKey`).
![](https://main.qcloudimg.com/raw/774299c4fa7afdc0db1247a7d26f02f4.png)

### Creating usage plan
1. On the left sidebar, click **[Usage Plan](https://console.cloud.tencent.com/apigateway/plan)** to enter the usage plan list page.
2. Click **Create** in the top-left corner and enter the configuration information as prompted.
3. Click **Submit** to complete the creation.

### Binding usage plan to key pair
1. On the **[Usage Plan](https://console.cloud.tencent.com/apigateway/plan)** page, click the ID of the target usage plan to enter the usage plan details page.
2. On the usage plan details page, click **Bind Key**.
3. Check the `SecretId` to be bound and click **Submit** to complete the binding.
![](https://main.qcloudimg.com/raw/774299c4fa7afdc0db1247a7d26f02f4.png)

### Binding usage plan to service environment
1. Select a created service on the **[Service](https://console.cloud.tencent.com/apigateway/service)** list page, switch to the Usage Plan tab, and click **Bind**.
![](https://main.qcloudimg.com/raw/a2c9314e9fb5fa9d72d8a5a7a8f2bebe.png)
2. In the usage plan binding window, select an effective environment and usage plan to be bound.
Effective environments: publish, pre-publish, and testing
3. Click **Submit** to complete the binding.
![](https://main.qcloudimg.com/raw/b831f08fab2563c4d07d175ffcb093c5.png)
>If two usage plans need to be bound to the same environment, they cannot be bound to the same key pair.

After the above steps are completed, the created `SecretId` and `SecretKey` can be provided to the end user who can be authenticated with the provided `SecretId` and `SecretKey` through the second-level domain name of the service (or a bound private domain name) to access the APIs published in the service.
