This document describes how to quickly run the Tencent Cloud TRTC Demo for WeChat Mini Program.

## Environment Requirements
- Minimum version of the WeChat app on iOS: 6.5.21
- Minimum version of the WeChat app on Android: 6.5.19
- Minimum version of the WeChat Mini Program base library: 1.7.0
- As the WeChat Developer Tool does not support native components (i.e., the &lt;live-pusher&gt; and &lt;live-player&gt; tags), you need to run the demo on a real device.


## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and click **Create Application**.
  If you already have an application, please note down its `SDKAppID` and then [download the SDK and demo source code](#step2) directly; otherwise, please proceed to the next step.
2. Enter the application's name and other information and click **OK**.
  After the application is created, an application ID (SDKAppID) will be automatically generated, which should be noted down.
![](https://main.qcloudimg.com/raw/1acc030cfc47e32bc36873c9a494b88a.png)

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Click the application card to enter the **Quick Start** page.
2. Click **WeChat Mini Program** in **Step 1: download SDK + auxiliary demo source code** to get redirected to [GitHub](https://github.com/tencentyun/TRTCSDK) (or visit [Gitee](https://gitee.com/cloudtencent/TRTCSDK)) and download the relevant SDK and demo source code.
![](https://main.qcloudimg.com/raw/486d7696aeb29e457bd654b5936a56e2.png)

<span id="step3"></span>
### Step 3. View and copy the encryption key
1. Click **View Key** in **Step 2: obtain the secret key to issue UserSig** to get the encryption key used to calculate `UserSig`.
2. Click **Copy Secret Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/d0b780f7b28833533e12807d1b11d8be.png)

<h3 id="CopyKey">Step 4. Configure demo project files</h3>

 The `GenerateTestUserSig.js` file in the demo project can be used to calculate `UserSig` locally by using the HMAC-SHA256 algorithm for quick demo execution.
 
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `WXMini/pages/webrtc-room/debug/GenerateTestUserSig.js` file.
3. Set the relevant parameters in the `GenerateTestUserSig.js` file:
  - SDKAPPID: please enter the actual `SDKAppID` obtained in [step 1](#step1).
  - SECRETKEY: please enter the actual key information obtained in [step 3](#step3).
  ![](https://main.qcloudimg.com/raw/c523de56afa69a7309872cbcfd75445f.png)

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166#Server).

### Step 5. Enable the category and push/pull tag permissions for WeChat Mini Program
Due to policy and compliance considerations, WeChat has not enabled the support for TRTC features (i.e., the &lt;live-pusher&gt; and &lt;live-player&gt; tags) for all WeChat Mini Programs:
- The WeChat Mini Program push/pull tags are supported only by organizational but not personal WeChat Mini Programs.
- The permission to use WeChat Mini Program push/pull tags is only available to certain [categories](https://developers.weixin.qq.com/miniprogram/dev/component/live-pusher.html).
- For WeChat Mini Programs in the eligible categories, you need to enable these component permissions in **[WeChat Official Accounts Platform](https://mp.weixin.qq.com) > **Development** > **API Settings** as shown below:
 ![](https://main.qcloudimg.com/raw/a5a9c121cd2dda0f879f97ba01922e15.png)

### Step 6. Compile and run
1. Launch the WeChat Developer Tool, select **WeChat Mini Program**, click the "Create" icon, and select **Import Project**.
2. Enter the `AppID` of your WeChat Mini Program and click **Import**.
 >!The `AppID` of your WeChat Mini Program should be entered here instead of the `SDKAppID`.
 >
 ![](https://main.qcloudimg.com/raw/b4eefa2896672e132f827fea79a2608b.jpg)
3. Click **Preview** to generate a QR code. Scan it with mobile WeChat to enter the WeChat Mini Program.

>! 
>- The &lt;live-player&gt; and &lt;live-pusher&gt; tags for WeChat Mini Program can only be used in mobile WeChat but not in the WeChat Developer Tool.
>- In order for the WeChat Mini Program to use the Tencent Cloud room management service, you need to enable the debugging feature in mobile WeChat: after scanning the QR code with mobile WeChat, tap **...** > **Enable Debugging** in the top-right corner.
![](https://main.qcloudimg.com/raw/79a3773337d34682b5f84f5694cd0290.jpg)

### Step 7. Release
1. Open the WeChat Mini Program Console and select **Development** > **Development Settings** > **Server Domain Name** to configure "valid domain names for requests"; otherwise, Tencent Cloud's room management service will not be available. The domain names that need to be configured are as shown below:
<table>
     <tr>
         <th nowrap="nowrap">Domain Name</th>  
         <th>Description</th>  
     </tr>
	 <tr>      
         <td>https://official.opensso.tencent-cloud.com</td>    
	      <td>Domain name for the WebRTC audio/video authentication service</td>   
     </tr> 
	 <tr>
	     <td>https://yun.tim.qq.com</td>   
	     <td>Domain name for the WebRTC audio/video authentication service</td>   
     </tr> 
	 <tr>      
	     <td>https://intl.cloud.tencent.com</td>   
	     <td>Push domain name</td>   
     </tr> 
		 	 <tr>      
	     <td>https://webim.tim.qq.com</td>   
	     <td>IM domain name</td>   
     </tr> 
</table>

 ![](https://main.qcloudimg.com/raw/693004574c9c17e86c36be2edf4db9a6.png)

2. Release the WeChat Mini Program as instructed in [Releasing WeChat Mini Programs](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/release.html#%E5%8F%91%E5%B8%83%E4%B8%8A%E7%BA%BF).

## FAQs
### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to click **Upgrade** in **Step 2: obtain the secret key to issue UserSig** to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm](https://intl.cloud.tencent.com/document/product/647/35166#.E8.80.81.E7.89.88.E6.9C.AC.E7.AE.97.E6.B3.95) ECDSA-SHA256.

### 2. What are the restrictions of the firewall?
As the SDK uses the UDP protocol for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.

### 3. Why should I enable debugging mode when debugging?
After debugging is enabled, you can skip adding "valid domain names for requests" to the WeChat Mini Program whitelist so as to avoid problems such as login failure and call connection failure.
