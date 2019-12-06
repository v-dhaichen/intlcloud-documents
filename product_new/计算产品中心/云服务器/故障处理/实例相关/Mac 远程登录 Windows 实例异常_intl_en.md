This document describes the common problems you may encounter when remotely logging in to a Windows CVM on Mac through Microsoft Remote Desktop and how to solve them.
## Problem Description

- When trying to remotely log in to a Windows CVM through Microsoft Remote Desktop, you get the message: “The certificate couldn't be verified back to a root certificate.”
<img src="https://main.qcloudimg.com/raw/070b9c862d6928988768b266461bc816.png" height="300" width="550" />
- When using Remote Desktop Connection on Mac, you get the message: “Remote Desktop Connection cannot verify the identity of the computer that you want to connect to.”


## Troubleshooting
> The following operations take Windows Server 2016 as an example.
>

### Logging in to the CVM using VNC

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the Instance page, find the CVM and click **Log in** as shown below:

3. In the “Log into Windows Instance” window, select “Alternative login methods (VNC)”, click **Log In Now** to log in to the CVM.
4. In the login window, select “Send CtrlAltDel” in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:


### Modifying the local group policy of the instance

1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press **Enter** to open the Local Group Policy Editor.
> You can also use the shortcut “Win+R” to open the Run box.
>
2. In the left navigation tree, select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Security**, double click **Require use of specific security layer for remote (RDP) connections** as shown below:

3. In the “Require use of specific security layer for remote (RDP) connections” window, select **Enabled**, and set the **Security Layer** to **RDP** as shown below:

4. Click **OK** to complete the configuration.
5. Restart the instance and try to make the connection again. If the connection fails again, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
