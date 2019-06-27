# 小米推送通道集成指南

小米推送通道是由**小米官方提供**的系统级推送通道。在小米手机上，推送消息能够通过小米的系统通道抵达终端，并且无需打开应用就能够收到推送。

## 获取小米推送秘钥


(a)根据[小米开放平台](https://dev.mi.com/console/appservice/push.html)指引开通小米开发者账号,然后注册应用并获取小米推送的秘钥。 

认证小米开发者：

![](/assets/认证小米开发者.jpeg)

获取小米推送密钥：

![](/assets/或者小米ID.jpeg)

## 配置小米推送相关内容
### AS开发建议使用jcenter依赖接入

1.配置包名。

```java
 manifestPlaceholders = [
	 PACKAGE_NAME:"应用包名"
        ]
```
2.引入小米推送的jar包
```js

/* 小米3.2.7-Release版
 * 注意：若小米通道使用此版本,则信鸽sdk版本也需要同时使用v3.2.7-Release
 */
 compile 'com.tencent.xinge:mipush:3.2.7-Release'

/*小米3.2.8-release版
 * 注意：若小米通道使用此版本,则信鸽sdk版本也需要同时使用v4.0.5
 */
 compile 'com.tencent.xinge:mipush:3.2.8-release'
```




### Eclipse开发接入

1.引入小米推送的jar包，可以在小米推送web官网[下载小米的jar包](https://dev.mi.com/mipush/downpage/)。


2.在配置好信鸽的基础上 ，新增小米推送的配置:

```xml
</application>
<service
android:name="com.xiaomi.push.service.XMPushService"
android:enabled="true"
android:process=":pushservice" />
<service
android:name="com.xiaomi.push.service.XMJobService"
android:enabled="true"
android:exported="false"
android:permission="android.permission.BIND_JOB_SERVICE"
android:process=":pushservice" />
<!-- 注：此service必须在3.0.1版本以后（包括3.0.1版本）加入 -->
<service
android:name="com.xiaomi.mipush.sdk.PushMessageHandler"
android:enabled="true"
android:exported="true" />
<service
android:name="com.xiaomi.mipush.sdk.MessageHandleService"
android:enabled="true" />
<!-- 注：此service必须在2.2.5版本以后（包括2.2.5版本）加入 -->
<receiver
android:name="com.xiaomi.push.service.receivers.NetworkStatusReceiver"
android:exported="true" >
<intent-filter>
<action android:name="android.net.conn.CONNECTIVITY_CHANGE" />

<category android:name="android.intent.category.DEFAULT" />
</intent-filter>
</receiver>
<receiver
android:name="com.xiaomi.push.service.receivers.PingReceiver"
android:exported="false"
android:process=":pushservice" >
<intent-filter>
<action android:name="com.xiaomi.push.PING_TIMER" />
</intent-filter>
</receiver>
</application>
<!-- 注：小米push 需要的权限 begin -->
<permission
android:name="应用包名.permission.MIPUSH_RECEIVE"
android:protectionLevel="signature" />
<!-- 这里com.example.mipushtest改成app的包名 -->

<uses-permission android:name="应用包名.permission.MIPUSH_RECEIVE" />
<!-- 这里com.example.mipushtest改成app的包名 -->
<!-- 注：小米push 需要的权限 end -->
```

3.在 ```AndroidManifest.xml``` 增加自定义 ```Receiver``` 配置如下：

```xml
<receiver
android:exported="true"
android:name="com.tencent.android.mipush.XMPushMessageReceiver">
<intent-filter>
<action android:name="com.xiaomi.mipush.RECEIVE_MESSAGE" />
</intent-filter>
<intent-filter>
<action android:name="com.xiaomi.mipush.MESSAGE_ARRIVED" />
</intent-filter>
<intent-filter>
<action android:name="com.xiaomi.mipush.ERROR" />
</intent-filter>
</receiver>

```
## 开启小米推送

设置小米APPID和APPKEY。

```java
XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
//打开第三方推送
XGPushConfig.enableOtherPush(getApplicationContext(), true);


//注册成功的日志如下
12-02 16:17:32.299 12584-12584/com.qq.xgdemo I/XINGE: [XGPushManager] Action -> Register to xinge server
12-02 16:17:32.996 12584-12584/com.qq.xgdemo I/XINGE: [XGPushManager] Register call back to com.qq.xgdemo
12-02 16:17:32.997 12584-12626/com.qq.xgdemo I/XINGE: [XGPushManager] XG register push success with token : 1d31bb3ea6185baebdf05dfc2e586dfe5dc41fb5
12-02 16:17:33.001 12584-12626/com.qq.xgdemo I/XINGE: [XGOtherPush] other push token is : YZQfRxmxdfNlbSKpNWCa3tM4Esnq6op4qeOsQO2qT88= other push type: xiaomi
```
**注：如果需要通过点击回调获取参数或者跳转自定义页面，可以通过使用Intent来实现，[点击查看教程](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95)**



## 代码混淆

```xml
-keep class com.xiaomi.**{*;}
-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

## 厂商通道测试方法(通用)

1. 在您的App中集成信鸽V3.2.1以上版本的SDK，并且按照「厂商通道集成指南」集成所需的厂商SDK

2. 确认已在信鸽管理台中「应用配置-厂商&海外通道」中填写相关的应用信息。通常相关<font color= darkblue>**配置将在1个小时后生效，请您耐心等待，在生效后再进行下一个步骤**</font>

3. 将集成好的App（测试版本）安装在测试机上，并且运行App

4. 保持App在前台运行，尝试对设备进行单推/全推

5. 如果应用收到消息，将App退到后台，并且杀掉所有App进程

6. 再次进行单推/全推，如果能够收到推送，则表明厂商通道集成成功