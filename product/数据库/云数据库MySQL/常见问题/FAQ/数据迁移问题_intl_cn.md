### 如何把本地的 sql 文件导入到 MySQL 数据库中？

**步骤1：**在[腾讯云控制台](https://console.cloud.tencent.com/)的左上角，单击【云产品】菜单下的【关系型数据库】，进入数据库产品页面。
![](https://main.qcloudimg.com/raw/0af4db8715dff80562105f951fece9fb.png)
**步骤2：**在关系型数据库页面中，单击【MySQL】下的【实例列表】，找到目标地域（此例中以广州为例）中要操作的状态为“未初始化” MySQL 数据库实例。
![](https://main.qcloudimg.com/raw/a69b73d296fc74cec0c96c4e680caa66.png)
**步骤3：**单击【初始化】对要操作的 MySQL 实例执行初始化。
![](https://main.qcloudimg.com/raw/945a4e69bef68eb706a520d4cbac13cf.png)
**步骤4：**配置初始化相关参数，然后单击【确定】开始初始化。
**支持的字符集** ：选择 MySQL 数据库支持的字符集。
**表名大小写敏感** ：表名是否大小写敏感，默认为是。
**自定义端口** ：数据库的访问端口，默认为 3306。
**root 账户密码**：新创建的 MySQL 数据库的用户名默认为 root，此处用来设置此 root 账户的密码。
**确认密码** ：再次输入密码。
![](https://main.qcloudimg.com/raw/8de4fc73cbc1e50f76546616958c24d0.png)

**步骤5：**目标 MySQL 实例的状态变为“运行中”，说明已初始化成功。
![](https://main.qcloudimg.com/raw/4ec53b759f51cdb63edc3dc7c83faa3e.png)

**步骤6：**单击操作里面的【管理】，然后单击【导入数据库】，选择导入文件，接下来选择目标数据库，最后确认导入（导入的单个 sql 文件不超过 2GB，文件名允许英文、数字，下划线）。
![](//mc.qcloudimg.com/static/img/5cf4795c885ea7a699dcf5b94a4a725e/image.png)

### 如何导出数据库数据？
1. 如果需要导出冷备数据，可在控制台实例【备份管理】下载。
2. 如果需要导出实时数据，可以购买只读实例，通过只读实例 mysqldump 获取。

### 原数据库大概 7G，哪种方式最快迁移至腾讯云购买的 MySQL 数据库中？
建议您使用 [数据迁移](https://cloud.tencent.com/document/product/571/8710) 功能，可以直接连到您的源库进行数据同步。

### 想配置同城双备，能够实现两个实例实时数据同步吗？如何做？
可以在控制台购买 [灾备实例](https://intl.cloud.tencent.com/document/product/236/7272) 来实现您这个需求 。

### 如何了解更多有关数据迁移、数据审计、数据订阅的问题？
详见 [数据迁移问题](https://cloud.tencent.com/document/product/571/13706)
详见 [数据审计问题](https://cloud.tencent.com/document/product/672/14403)
详见 [数据订阅问题](https://cloud.tencent.com/document/product/571/13707)
