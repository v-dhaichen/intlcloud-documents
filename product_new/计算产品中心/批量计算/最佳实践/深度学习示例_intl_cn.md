## 快速开始
本文介绍一个基于 scikit-learn 机器学习库，编写一个多层感知器（MLP，Multilayer Perceptron）BP 算法的深度学习示例。通过对历史国际足球比赛、球队排名、球员体能技术指标以及 FIFA 2018 小组赛结果建模，预测两只球队的胜负平概率。具体操作步骤如下：
### 一. 制作自定义镜像
1. 制作步骤参考 [创建自定义镜像](https://inll.cloud.tencent.com/zh/document/product/213/4942) 文档。
2. 安装依赖包，以 Centos 7.2 64 bit 为例：
```
yum -y install gcc
yum -y install python-devel
yum -y install tkinter
yum -y install python-pip
pip install --upgrade pip
pip install pandas
pip install numpy
pip install matplotlib
pip install seaborn
pip install sklearn
pip install --upgrade python-dateutil
```

### 二. 下载程序包
单击 [下载程序压缩包](https://main.qcloudimg.com/raw/40b6eb7103072ca549e398ca39783f21.gz)，下载完成后上传压缩包至 [对象存储](https://intl.cloud.tencent.com/zh/document/product/436)。通过指定程序包的对象存储地址，Batch 会在作业运行前下载压缩包到云服务器，自动解压后执行。

### 三. 创建 “fifa-predict” 任务模板
1. 登录 [批量计算控制台](https://console.cloud.tencent.com/batch/task)，单击左侧导航栏【任务模板】选项，选择目标地域后，单击【新建】按钮。

2. 配置基本信息。示例如下：
![](https://main.qcloudimg.com/raw/adbdbc31286ef4d58d3ade44570cf832.png)
  * 名称：fifa-predict。
  * 描述：数据训练与预测。
  * 资源配置：S2.SMALL1（1核1G），公网带宽按量收费。
  * 资源数量：并发渲染数，例如3台，并行训练3个神经网络模型。
  * 超时时间：默认值。
  * 重试次数：默认值。
  * 镜像：自定义镜像标识符，例如 img-i64lx84h。

3. 配置程序信息。示例如下：
![](https://main.qcloudimg.com/raw/1203aa789d6666d7b63db9d643f1bb38.png)
  * 执行方式：PACKAGE。
  * 程序包地址：以对象存储举例，`cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`。
  * Stdout 日志：格式参考 [COS、CFS 路径填写](https://intl.cloud.tencent.com/zh/document/product/599/13996)。
  * Stderr 日志：同 Stdout 日志。
  * 命令行：`python predict.py "Japan" "Senegal"`。

4. 球队列表：'Russia', 'Saudi Arabia', 'Egypt', 'Uruguay', 'Portugal', 'Spain', 'Morocco', 'Iran', 'France', 'Australia', 'Peru', 'Denmark', 'Argentina', 'Iceland', 'Croatia', 'Nigeria', 'Brazil', 'Switzerland', 'Costa Rica', 'Serbia', 'Germany', 'Mexico', 'Sweden', 'Korea Republic', 'Belgium', 'Panama', 'Tunisia', 'England', 'Poland', 'Senegal', 'Colombia', 'Japan'。

5. 配置存储映射（略过）。

6. 预览任务 JSON 文件，确认无误后，单击【保存】按钮。

### 四. 创建 “fifa-merge” 任务模板
1. 登录 [批量计算控制台](https://console.cloud.tencent.com/batch/task)，单击左侧导航栏【任务模板】选项，选择目标地域后，单击【新建】按钮。

2. 配置基本信息。示例如下：
![](https://main.qcloudimg.com/raw/3f79fc57b16a7a3c6d5d1083e86576e2.png)
  * 名称：fifa-merge。
  * 描述：预测数据汇总。
  * 资源配置：S2.SMALL1（1核1G），公网带宽按量收费。
  * 资源数量：1台。
  * 超时时间：默认值。
  * 重试次数：默认值。
  * 镜像：自定义镜像标识符，例如 img-i64lx84h。

3. 配置程序信息。示例如下：
![](https://main.qcloudimg.com/raw/7c08ee74a2dadbea3ef0bc3b94788694.png)
  * 执行方式：PACKAGE。
  * 程序包地址：以对象存储举例，`cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`。
  * Stdout 日志：格式参考 [COS、CFS 路径填写](https://intl.cloud.tencent.com/zh/document/product/599/13996)。
  * Stderr 日志：同 Stdout 日志。
  * 命令行：`python merge.py /data`。

4. 配置存储映射。
![](https://main.qcloudimg.com/raw/eb1b1dd75a45c81ae4b7089b36f7adc9.png)
 - 输入路径映射 > COS/CFS路径：填写“fifa-predict”模板 Stdout 日志路径。
 - 输入路径映射 > 本地路径：/data。

5. 预览任务 JSON 文件，确认无误后，单击【保存】按钮。

### 五. 提交作业
1. 单击左侧导航栏【作业】选项，选择目标地域后，单击【新建】按钮。

2. 配置作业基本信息。示例如下：
  * 作业名称：fifa。
  * 优先级：默认值。
  * 描述：fifa 2018 model。

3. 选中任务流页面左侧 **fifa-predict** 和 **fifa-merge** 任务，移动鼠标将任务放置到右侧画布中。单击 **fifa-predict** 任务拖拽箭头到 **fifa-merge** 任务。
![](https://main.qcloudimg.com/raw/d92616232f162679f03edfb4b7e32188.png)

4. 打开任务流右侧 **任务详情**，确认配置无误后，单击【完成】按钮。

5. 查询作业运行信息，参考 [查询信息](https://intl.cloud.tencent.com/zh/document/product/599/14567)。
![](https://main.qcloudimg.com/raw/7f2fac7290ca2c51f0203e7b01821354.png)

6. 渲染结果查询，参考 [查看对象信息](https://intl.cloud.tencent.com/zh/document/product/436/13326)。
![](https://main.qcloudimg.com/raw/1f8434915088871fa540ff7b754f84a1.png)

## 下一步可以干什么？
本文列举了一个简单的机器学习示例，仅仅是向用户展示最基本的能力，您可以根据控制台使用指南继续测试 Batch 更高阶的能力。
- **丰富的云服务器配置**：Batch 提供了丰富的云服务器 CVM 配置项，您可以根据业务场景自定义 CVM 配置。
- **远程存储映射**：Batch 在存储访问上进行优化，将对远程存储服务的访问简化为对本地文件系统操作。
- **并行训练多个模型**：Batch 支持指定并发数，通过 [环境变量](https://intl.cloud.tencent.com/zh/document/product/599/11752) 区分不同的并发实例，每个实例读取不同的训练数据，实现并行建模。
