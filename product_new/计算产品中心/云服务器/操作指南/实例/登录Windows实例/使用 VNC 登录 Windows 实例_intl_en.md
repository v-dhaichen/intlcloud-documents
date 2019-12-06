## Scenario

VNC login is a browser-based method of CVM remote connection that Tencent Cloud offers its users. When a client does not have remote login installed or cannot use it and in the situation where login cannot be accomplished by any other means, the user can connect to a CVM using VNC login and observe the CVM’s status and can also do basic CVM management operations using the CVM account.    

## Use Limits

- The features of copy/paste, Chinese input, and file upload/download are currently not supported on CVMs using VNC login. 
- Main scream browsers must be used when using VNC login of a CVM, such as Chrome, Firefox, and IE 10 or above.
- A VNC login is a dedicated terminal, meaning that only one user at a time can use a VNC login.

## Applicable OS

Windows, Linux, or macOS.

##  Prerequisites

You must already have admin account/password for the Windows instance  to be logged in to.
- If you use a system default password to log in to the instance, then go to [internal message](https://console.cloud.tencent.com/message) to get it.
If you forgot the password, then [reset instance password](http://intl.cloud.tencent.com/document/product/213/16566).

## Steps

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance’s management page, select the Windows CVM that you want to log in to and click **Log In**, as shown below:
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. In the **Log into Windows Instance** pop-up window, select **Other login method (VNC)** and click **Log in now**, as shown below.
![](https://main.qcloudimg.com/raw/9f964c1ebdec90f7e371b42340e13662.png)
4. In the login window, select “Send Remote Command” in the top left corner, and press **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/c07755c1e0d0040e2ecb87f048b8be1b.png)



