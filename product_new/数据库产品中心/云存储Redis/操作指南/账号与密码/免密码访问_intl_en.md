TencentDB for Redis supports both password-enabled and password-free access. To use password-free access mode, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.


>- For the sake of data security, you are not recommended to enable password-free access.
>- After password-free access is enabled, you are recommended to limit the number of accessing servers using a security group.

## Setting Password-free Access
#### Select password-free access when creating an instance
 1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and click **Create Instance**.
 2. Select **Password Exemption Authentication** in the **Set Password** option on the instance creation page. After the instance is created successfully, it can be accessed without password.
![](https://main.qcloudimg.com/raw/03a688ea981ccaf28124b74ebb8d9223.png)

#### Enable password-free access for existing instances
In the instance list, click an instance name to enter the **Instance Details** page, and click **Password Exemption Access** in **Configuration Info** > **Connection Password**.

## Viewing Password-free Access Status
In the instance list, click an instance name to enter the **Instance Details** page where you can view whether the instance has enabled password-free access.
![](https://main.qcloudimg.com/raw/ddd227bf61e70cb72e3971ea58c9d773.png)

## Disabling Password-free Access
In **Configuration Info** > **Connection Password**, click **Reset Password** to disable password-free access.

