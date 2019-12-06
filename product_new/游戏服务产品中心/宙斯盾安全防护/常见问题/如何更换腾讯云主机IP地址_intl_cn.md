若云服务器公网 IP 地址遭受到 DDoS 攻击，说明当前公网 IP 地址已经暴露。因此需要在接入高防 IP 后，更换已经暴露的公网 IP 地址，以避免攻击者绕过 DDoS 高防 IP，继续直接攻击主机 IP 地址。

如需更换云服务器的公网 IP 地址，详情请参见如下操作步骤：

## 一、 腾讯云服务器转弹性 IP
若当前云服务器的公网 IP 地址还不是弹性公网 IP，则需要先转换为弹性公网 IP 地址，以便于在更换后继续保留该 IP。
首先，进入 [腾讯云服务器控制台](https://console.cloud.tencent.com/cvm/overview)。在 “主IP地址列” 下，单击 “转换为弹性 IP” 按钮，单击【确定转换】。
![](https://main.qcloudimg.com/raw/b4490387ec3c6b2d1760c671c8deee61.jpg)

>**说明：**
>将当前公网 IP转换为弹性 IP 地址，转发过程不会中断服务。

## 二、 弹性 IP 转公网 IP
在 “操作” 列 “更多” 下，选择 “IP 操作” 里的 “解绑弹性 IP”，并同时勾选 “解绑后免费分配公网 IP”，单击 【确定】。此时云服务器的 IP 已更为新的公网 IP 地址。
![](https://main.qcloudimg.com/raw/99ab9c140353df2e301b3d1ce99f75d6.jpg)
![](https://main.qcloudimg.com/raw/2874632e88dcb789e63b23fd78a1076e.jpg)

>**注意：**
>若用户的云服务器已经使用了弹性公网 IP，则可以直接绑定为其他已有的弹性公网 IP。

在选择第一步操作时，将单击 【确定转换】变为单击 【其他弹性公网 IP】；立即跳转到 “绑定弹性公网 IP”，单击 "选择弹性公网 IP" 框，选择好 IP，单击【确认】，即为云服务器分配了新的公网 IP 地址。
![](https://main.qcloudimg.com/raw/300d9ef45330d9e4b614a5eeb8d4ce04.jpg)
![](https://main.qcloudimg.com/raw/8ecef895f103b989b2f0a7065951b3b2.jpg)
