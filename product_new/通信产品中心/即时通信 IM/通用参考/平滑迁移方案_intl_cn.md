即时通信 IM 拥有丰富的高并发、高可靠的运营经验。如果正在使用自主研发或第三方即时通信服务的 App 开发者希望接入即时通信 IM，则需要考虑迁移问题。即时通信 IM 根据不同的场景提出了针对性迁移方案。

## 术语约定

后续文档中，我们约定：

- **老系统：**App 原本使用的即时通信服务。
- **新系统：**腾讯云的即时通信 IM 服务。
- **App 1.0：**基于老系统来实现即时通信功能的 App。
- **App 2.0：**基于新系统来实现即时通信功能的 App。
- **消息路由（消息回调）服务：**第三方通信服务商在收到消息后，向 App 后台转发一份消息，类似于即时通信 IM 的 [发单聊消息之后回调](https://intl.cloud.tencent.com/document/product/1047/34365)。

迁移过程本质上就是将即时通信服务后台从老系统切换到新系统，并将 App 1.0 升级到 App 2.0 的过程。

## 迁移方案

即时通信 IM 为您提供以下两种备选迁移解决方案，不同方案的迁移效果不同，实施难度也相差很大，需要综合考虑 App 现有的即时通信实现场景来确定合理的迁移方案。

### 强制升级方案

强制升级策略是指完成即时通信 IM 数据同步后，强制 App 从1.0升级为2.0，此方案实施简单，升级后无需处理新老 App 兼容问题。具体方案如下图所示：
![](https://main.qcloudimg.com/raw/e37a5686c81c73827c20312169c3ecc0.png)

主要流程如下：

1. 导入历史数据至即时通信 IM，包括：
   - 导入帐号
   - 导入用户资料
   - 导入用户关系链
   - 导入单聊历史消息
   - 导入群组数据
   - 导入群聊历史消息
2. 强制用户从 App 1.0 升级到 App 2.0。
3. 老系统下架，所有用户通信均在新系统进行。

### 新老兼容方案

新老 App 可以共存，消息互通，在 App 1.0 停用之前，App 后台需要在新老系统之间保持实时双向同步，此方案相对复杂，对终端用户体验更好。具体方案如下图所示：
![](https://main.qcloudimg.com/raw/3b19fed85458fa96ae7110fea8cb8e41.png)

主要流程如下：

1. 导入历史数据至即时通信 IM，包括：
   - 导入帐号
   - 导入用户资料
   - 导入用户关系链
   - 导入单聊历史消息
   - 导入群组数据
   - 导入群聊历史消息
2. 双向同步 App 新老系统数据，包括：
   - 实时同步单聊消息
   - 实时同步群组数据和群聊消息
3. 新老系统共存，消息互通，待老 App 自然消亡。

## 详细迁移操作

### 导入帐号

导入帐号是后续各种数据导入的前提。
App 后台需要调用 [批量帐号导入 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34954) 将原有帐号全部导入到即时通信 IM，如需在导入帐号的同时导入用户昵称和头像，则需调用 [单个帐号导入 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34953)。

### 导入用户资料

调用 [设置资料 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34916) 将存量的用户资料导入即时通信 IM。

### 导入用户关系链

调用 [添加好友 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34902) 将存量的关系链导入即时通信 IM。

### 导入单聊历史消息

调用 [导入单聊消息 REST 接口](https://intl.cloud.tencent.com/document/product/1047/35014) 将存量的单聊消息导入即时通信 IM。

### 导入群组数据和群聊历史消息

导入群组数据、群聊历史消息应当遵循以下流程：

1. 调用 [导入群基础资料 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34967) 创建群组，调用该接口时可以指定初始群成员。
2. 如果导入群时没有导入群成员，可以调用 [导入群成员 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34969) 导入群成员。
3. 调用 [导入群消息 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34968) 导入历史群聊消息。
4. 如果需要修正群成员的未读消息数量，可以调用 [设置成员未读消息计数 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34909) 进行相关操作。

单聊消息、群组数据和群聊消息都需要托管到新系统。当新系统中产生这种类型的增量数据时，使用即时通信 IM 的回调同步到老系统中。同时，老系统中产生的增量数据也需要同步到新系统。

### 同步单聊消息

老系统中增量消息时通过调用 [单发单聊消息 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34919) 同步到即时通信 IM，即时通信 IM 中增量消息时通过调用 [发单聊消息之后回调](https://intl.cloud.tencent.com/document/product/1047/34365)同步到老系统。

### 同步群组数据和群聊消息

**同步群组资料**

1. 老系统中群组基本资料的变更，需要通过调用 [修改群组基础资料 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34962) 进行实时同步。
2. 即时通信 IM 中群组基本资料的变更，需要通过调用 [创建群组之后回调](https://intl.cloud.tencent.com/document/product/1047/34368)、[群组解散之后回调](https://intl.cloud.tencent.com/document/product/1047/34377) 和 [群组资料修改之后回调](https://intl.cloud.tencent.com/document/product/1047/34378) 同步到老系统。

**同步群成员信息**

1. 老系统中成员的增删，需要通过调用 [增加群组成员 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34921) 和 [删除群组成员 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34949) 同步到即时通信 IM。
2. 即时通信 IM 中成员的进出群信息通过 [新成员入群之后回调](https://intl.cloud.tencent.com/document/product/1047/34372) 和 [群成员离开之后回调](https://intl.cloud.tencent.com/document/product/1047/34373) 同步到老系统。

**同步群消息**

1. 老系统中的增量群聊消息，需要通过调用群组中 [在群组中发送普通消息 REST 接口](https://intl.cloud.tencent.com/document/product/1047/34959) 同步到即时通信 IM。
2. 即时通信 IM 中的增量群聊消息，需要通过 [群内发言之后回调](https://intl.cloud.tencent.com/document/product/1047/34375) 同步到老系统。

>若无法涵盖 App 现有的即时通信服务，您可以联系客服或者商务经理一起协商合理的迁移方案。
