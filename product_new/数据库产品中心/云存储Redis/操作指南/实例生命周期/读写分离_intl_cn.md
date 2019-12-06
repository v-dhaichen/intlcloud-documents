## 操作场景
云数据库 Redis 支持开启和关闭读写分离功能，针对读多写少的业务场景，解决热点数据集中的读需求，最大支持1主5从模式，提供最大5倍的读性能扩展能力。

>开启读写分离，将对只读副本收取一定的费用，具体费用请参见 [产品定价](https://intl.cloud.tencent.com/document/product/239/9894)。

## 操作步骤
1. 登录 [云数据库 Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在实例列表页中，选择需要创建只读实例的云数据库，单击实例名称，进入实例详情页。
3. 在【节点管理】页，单击副本只读按钮，开启读写分离。
![](https://main.qcloudimg.com/raw/31acc5f160e4b4160f9b79a890990200.png)

