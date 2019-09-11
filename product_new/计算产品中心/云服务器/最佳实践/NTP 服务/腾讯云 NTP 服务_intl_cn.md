网络时间协议（Network Time Protocol，NTP）是用于同步网络中各个计算机的时间的协议。其用途是把计算机的时钟同步到世界协调时 UTC，NTP 设计时考虑到了各种网络延迟，通过公共网络同步时，误差可以降低到 10 毫秒以内；通过本地网络同步时，误差可以降低到 1 毫秒。

腾讯云提供了内网 NTP 服务器供腾讯云内网设备使用，对于非腾讯云设备，可以使用腾讯云提供的公网 NTP 服务器。

### 内网 NTP 服务器

```
ntpupdate.tencentyun.com
```

### 外网 NTP 服务器

```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```



