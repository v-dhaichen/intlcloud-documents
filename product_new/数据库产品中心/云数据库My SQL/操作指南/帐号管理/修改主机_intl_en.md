## Operation Scenario
By modifying the host address authorized by the database account in the TencentDB for MySQL Console, you can control client access to the database so as to improve access security.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance to be modified and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select **Database Management** > **Account Management**, find the account for which to modify the host, and select **More** > **Modify Host**.
![](https://main.qcloudimg.com/raw/9f6a4add3bde860cde8c9565f4f0a3d5.png)
4. In the pop-up dialog box for modifying host, enter the new host address and click **OK**.
>The host address may come in the format of IP address. To allow all clients to access the database using the database account, enter %.
>
![](https://main.qcloudimg.com/raw/113ed501aa7687c9812da29e9314daeb.png)


