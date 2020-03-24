## 简介

您可以通过对象存储控制台，对存储桶设置服务端加密，这样可以实现对新上传到该存储桶的对象默认进行加密。关于存储桶加密的详细信息，请参见 [存储桶加密概述](https://intl.cloud.tencent.com/document/product/436/33457)。

>目前存储桶的加密方式支持 SSE-COS 加密（即由 COS 托管密钥的服务端加密）。关于服务端加密的介绍，请参见 [服务端加密概述](https://intl.cloud.tencent.com/document/product/436/18145?lang=en)。


## 操作步骤
#### 在新创建存储桶时设置加密

您可以在 [创建存储桶](https://intl.cloud.tencent.com/document/product/436/13309) 时添加存储桶加密，如下图所示：
![](https://main.qcloudimg.com/raw/cc4f781f6ffa98b3786e52cf84d5c8d4.png)



#### 在已创建存储桶中设置加密

若您在创建存储桶时未设置加密，您可以按照下述步骤为存储桶设置加密。

1. 在 [存储桶列表](https://console.cloud.tencent.com/cos5/bucket) 页，找到您需要设置加密的存储桶，单击其名称，进入存储桶配置页面。
2. 单击左侧的【基础配置】，进入存储桶基础配置页。
3. 下拉页面找到【存储桶加密】配置项，单击【编辑】，将当前状态修改为“开启”。
![](https://main.qcloudimg.com/raw/e2863ba89860f15464870ac198b5335f.png)
4. 选择指定的加密方式，然后单击【保存】即可完成存储桶加密配置。
![](https://main.qcloudimg.com/raw/524717e180e357eb74fa8be0b42a51a3.png)
