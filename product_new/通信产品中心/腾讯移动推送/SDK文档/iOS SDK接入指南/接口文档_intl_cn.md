


## 启动腾讯移动推送推送服务

#### 接口说明
通过使用在腾讯移动推送官网注册的应用信息，启动腾讯移动推送服务。

```objective-c
- (void)startXGWithAppID:(uint32_t)appID appKey:(nonnull NSString *)appKey delegate:(nullable id<XGPushDelegate>)delegate ;
```

#### 参数说明
- AppID：通过前台申请的应用 ID， 即 Access ID。
- AppKey： 通过前台申请的 appKey，即 Access Key。
- Delegate：回调对象。 

>接口所需参数必须要正确填写，反之腾讯移动推送服务将不能正确为应用推送消息。

#### 示例代码
```Objective-C
[[XGPush defaultManager] startXGWithAppID: <#your access ID#>appKey:<#your access key#> delegate:<#your delegate#>];
```

## 终止腾讯移动推送服务

#### 接口说明
终止腾讯移动推送服务后，将无法通过腾讯移动推送服务向设备推送消息，如再次需要接收腾讯移动推送服务的消息推送，则必须需要再次调用 `startXGWithAppID:appKey:delegate:` 方法重启腾讯移动推送服务。
```objective-c
- (void)stopXGNotification;
```

#### 示例代码
```Objective-C
[[XGPush defaultManager] stopXGNotification];
```

## 自定义通知栏消息行为

### 创建消息支持的行为

#### 接口说明
在通知消息中创建一个可以点击的事件行为。

```objective-c
+ (nullable id)actionWithIdentifier:(nonnull NSString *)identifier title:(nonnull NSString *)title options:(XGNotificationActionOptions)options;
```

#### 参数说明
- identifier：行为唯一标识。 
- title：行为名称。 
- options：行为支持的选项。


#### 示例代码
```objective-c
XGNotificationAction *action1 = [XGNotificationAction actionWithIdentifier:@"xgaction001" title:@"xgAction1" options:XGNotificationActionOptionNone];
```

>通知栏带有点击事件的特性，只有在 iOS8.0 + 以上支持，iOS 7.x or earlier 的版本，此方法返回空。

### 创建分类对象

#### 接口说明
创建分类对象，用以管理通知栏的 Action 对象。
```objective-c
+ (nullable id)categoryWithIdentifier:(nonnull NSString *)identifier actions:(nullable NSArray<XGNotificationAction *> *)actions intentIdentifiers:(nullable NSArray<NSString *> *)intentIdentifiers options:(XGNotificationCategoryOptions)options;
```

#### 参数说明
- identifier：分类对象的标识。
- actions：当前分类拥有的行为对象组。
- intentIdentifiers：用以表明可以通过 Siri 识别的标识。
- options：分类的特性。

>通知栏带有点击事件的特性，只有在iOS8+以上支持，iOS 8 or earlier的版本，此方法返回空。


#### 示例代码
```Objective-C
XGNotificationCategory *category = [XGNotificationCategory categoryWithIdentifier:@"xgCategory" actions:@[action1, action2] intentIdentifiers:@[] options:XGNotificationCategoryOptionNone];
```

### 创建配置类
#### 接口说明
管理推送消息通知栏的样式和特性。
```objective-c
+ (nullable instancetype)configureNotificationWithCategories:(nullable NSSet<XGNotificationCategory *> *)categories types:(XGUserNotificationTypes)types;
```

#### 参数说明
- categories：通知栏中支持的分类集合。 
- types：注册通知的样式。

#### 示例代码
```objective-c
XGNotificationConfigure *configure = [XGNotificationConfigure configureNotificationWithCategories:[NSSet setWithObject:category] types:XGUserNotificationTypeAlert|XGUserNotificationTypeBadge|XGUserNotificationTypeSound];
```


## 角标自动加1

#### 接口说明
调用此接口上报当前 App 角标数到腾讯移动推送服务器，客户端配置完成即可使用“iOS 角标自动加1”的功能，此功能在管理台位置（创建推送 > 通知栏消息 > 常用设置 > 角标数字）。

```objective-c
- (void)setBadge:(NSInteger)badgeNumber;
```

#### 参数说明
badgeNumber： 应用的角标数。

 
>此接口必须本地调用，否则管理台使用“iOS 角标自动加1”功能时，角标会默认不变。  


#### 示例代码
```Objective-C
[[XGPush defaultManager] setBadge:7];
```

## 管理应用角标

#### 接口说明
管理 App 显示的角标数量，此接口需要在主线程中调用。
```objective-c
@property (nonatomic) NSInteger xgApplicationBadgeNumber;
```

#### 示例代码
```objective-c
// 设置应用角标
[[XGPush defaultManager] setXgApplicationBadgeNumber:0];

// 获取应用角标
NSInteger number = [[XGPush defaultManager] xgApplicationBadgeNumber];
```



## 管理设备 Token

### 查询设备 Token

#### 接口说明
查询当前应用从 APNs 获取的 Token 字符串。
```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *deviceTokenString;
```

#### 示例代码
```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] deviceTokenString];
```


### 查询 XGToken
#### 接口说明
查询当前应用从腾讯移动推送服务器生成的 Token 字符串。
```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *xgTokenString;
```

#### 示例代码
```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] xgTokenString];
```




### 查询 APNs 注册结果

#### 接口说明
如果注册成功，则应用会调用 `UIApplicationDelegate` 代理对象的回调方法\(如下\)。

```Objective-C
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken;
```

### 查询腾讯移动推送注册结果

#### 接口说明
SDK 的启动方法自动注册设备从 APNs 获取的 Token 到腾讯移动推送服务器，注册结果会在 `XGPushDelegate` \(以下\)的回调方法返回。


```objective-c
- (void)xgPushDidRegisteredDeviceToken:(NSString *)deviceToken error:(NSError *)error;
```

>此回调方法在注册成功之后调用，当前的 Token 已注册过后，SDK 将缓存注册信息，此方法将不会再调用。

### 绑定/解绑标签和账号

#### 接口说明
开发者可以针对不同的用户绑定标签，然后对该标签进行推送。

>此接口应在 xgPushDidRegisteredDeviceToken:error: 返回正确后被调用。

#### 单操作接口 
```Objective-C
- (void)bindWithIdentifier:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
- (void)unbindWithIdentifer:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
```

#### 参数说明
- identifier：标签或账号。
- type：绑定类型。

#### 示例代码
```Objective-C
//绑定标签：
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your tag" type:XGPushTokenBindTypeTag];

//解绑标签
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your tag" type:XGPushTokenBindTypeTag];

//绑定账号：
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your account" type:XGPushTokenBindTypeAccount];

//解绑账号：
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your account" type:XGPushTokenBindTypeAccount];
```

####  批量操作接口

```Objective-C
- (void)bindWithIdentifiers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type
- (void)unbindWithIdentifers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type;
```

#### 参数说明
- identifiers：标签或账号列表。
- type：绑定类型。


>标签或账号字符串不允许有空格或者是 tab 字符。。

### 批量更新标签/账号

#### 接口说明
覆盖原有的标识（标签/账号），若之前没有绑定标识，则会执行新增标识。

>此接口应在 xgPushDidRegisteredDeviceToken:error: 返回正确后被调用。

```Objective-C
- (void)updateBindedIdentifiers:(nonnull NSArray <NSString *> *)identifiers bindType:(XGPushTokenBindType)type;
```
####  参数说明 
- identifiers：标签标识字符串数组，标签字符串不允许有空格或者是 tab 字符。
- type：标识类型。


>若指定为标签类型，此接口会将当前 Token 对应的旧有的标签全部替换为当前的标签；若指定账号类型，此接口仅取 identifiers 列表中第一个。

### 清除全部标签/账号

#### 接口说明
根据标识类型，清除所有标识。

>此接口应在 xgPushDidRegisteredDeviceToken:error: 返回正确后被调用。

```Objective-C
- (void)clearAllIdentifiers:(XGPushTokenBindType)type;
```
**参数说明**
type：标识类型。


### 查询绑定的标签和账号
#### 接口说明
根据指定类型查询当前 Token 对象绑定的标识。

>此接口应在 xgPushDidRegisteredDeviceToken:error: 返回正确后被调用。

```objective-c
- (nullable NSArray<NSString *> *)identifiersWithType:(XGPushTokenBindType)type;
```

#### 示例代码
```objective-c
// 查询标签
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeTag];
// 查询账号
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeAccount];
```

## 查询设备通知权限

#### 接口说明
查询设备通知权限是否被用户允许。 


```objective-c
- (void)deviceNotificationIsAllowed:(nonnull void (^)(BOOL isAllowed))handler;
```

#### 参数说明
handler：查询结果的返回方法。


#### 示例代码
```objective-c
[[XGPush defaultManager] deviceNotificationIsAllowed:^(BOOL isAllowed) {
        <#code#>
    }];
```

## 查询 SDK 版本
#### 接口说明
查询当前 SDK 的版本。

```objective-c
- (nonnull NSString *)sdkVersion;
```

#### 示例代码
```objective-c
[[XGPush defaultManager] sdkVersion];
```


## 日志上报接口

#### 接口说明
开发者如果发现推送相关功能异常，可以调用该接口，触发本地 push 日志的上报，反馈问题时，请将文件地址提供给我们，便于排查问题。
```
- (void)uploadLogCompletionHandler:(nullable void(^)(BOOL result,  NSString * _Nullable errorMessage))handler;
```
#### 参数说明
-  @brief：上报日志信息 （SDK1.2.4.1+）。
-  @param handler：上报回调。

#### 示例代码
```
[[XGPush defaultManager] uploadLogCompletionHandler:nil];
```

## 免费集群反注册

#### 接口说明
背景：App 如果从免费集群迁移到付费集群，在两个集群同时推送，可能会出现重复消息。因此需要调用此接口，SDK 会把设备信息在免费集群进行反注册。  
引入头文件：XGForFreeVersion.h，在startXGWithAppID 之前调用
```
@property uint32_t freeAccessId;
```
#### 参数说明
-  @freeAccessId 免费集群的 accessId（SDK1.2.5.3+）。

#### 示例代码
```
[XGForFreeVersion defaultForFreeVersion].freeAccessId = 2200262432;
```



## 本地推送
本地推送相关功能请参考 [苹果开发者文档](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SchedulingandHandlingLocalNotifications.html#//apple_ref/doc/uid/TP40008194-CH5-SW1)。






