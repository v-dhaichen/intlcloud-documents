**This document applies to iOS TPNS <font color="#FF0000">SDK v1.0+ and higher </font>**

## iOS Extension SDK API (iOS 10+)
**Report receipt of push messages. This API is used to check if push messages reach the devices.**
```objective-c
/**
  @brief    TPNS handles the message arriving at the device            
  @param request   Push request
  @param appID   TPNS app ID
  @param handler    Receipt of message handling, which is the rich media file associated in the callback method               
  @note            The associated rich media file, which you need to set the full URL address of the resource for in the push frontend and will be automatically downloaded in the SDK internally.        
*/
  - (void)handleNotificationRequest:(nonnull UNNotificationRequest *)request
  appID:(uint32_t)appID contentHandler:(nullable void(^)( NSArray
  <UNNotificationAttachment *>* _Nullable attachments,  NSError * _Nullable
  error))handler;
```
**Note:
Follow the steps below to use the extension SDK.**

1.Add Target
![](https://main.qcloudimg.com/raw/59828c0ecbfc4ea3def2efef3284c9bf.jpg)

2.Configure Target and add dependent library files: libXGExtension.a, libz.tbd, libsqlite3.tbd

![](https://main.qcloudimg.com/raw/4d217269058f55d5d344460222dafc71.jpg)
3.Call the SDK's statistics reporting API
**Example**

```Objective-C
- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request
  withContentHandler:(void (^)(UNNotificationContent *
  _Nonnull))contentHandler {
      [[XGExtension defaultManager] handleNotificationRequest:request appID:
  <#your xg AppID#> contentHandler:nil];
      self.contentHandler = contentHandler;
      self.bestAttemptContent = [request.content mutableCopy];
      self.contentHandler(self.bestAttemptContent);
      }
```






