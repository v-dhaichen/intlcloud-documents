
该操作指南以 Python 为例，其它编程语言类似。

## 前期准备
- 依赖环境：Python 2.7 - 3.x版本。
- KMS 产品服务开通：从 腾讯云控制台 开通KMS产品。
- 云 API 密钥服务开通：获取 SecretID、SecretKey 以及调用地址（endpoint），endpoint 一般形式为`*.tencentcloudapi.com`，例如 KMS 的调用地址为`kms.tencentcloudapi.com`，具体参考各产品说明。
- SDK 安装，执行以下命令，详细可参见 [tencentcloud-sdk-python github](https://github.com/TencentCloud/tencentcloud-sdk-python) 项目。
```
pip install tencentcloud-sdk-python
```


##  操作流程
您可以通过以下4个步骤完成敏感数据加密的操作。

1. 通过控制台 Console 或 API（CreateKey）创建一个用户主密钥 CMK，即创建用户主密钥 CMK。
2. 通过 API 调用 KMS 加密接口（Encrypt）将用户敏感数据进行加密，获取密文。
3. 根据业务需求将密文数据存储。
4. 读取数据时，通过 API 调用 KMS 解密接口（Decrypt）解密成明文。

## 操作步骤

### 步骤1：创建用户主密钥 CMK
用户主密钥的创建方式请参见 [创建密钥](https://intl.cloud.tencent.com/document/product/1030/31971) 文档。


### 步骤2：敏感信息加密

#### 前提条件：确保步骤1创建的用户主密钥为启用状态。

#### 控制台方式
在线工具适合处理单次或者非批量的加解密操作，例如首次生成密钥密文，开发者无需为非批量的加解密操作而去开发额外的工具，将精力集中在实现核心业务能力上，详情请参见 [加密解密](https://intl.cloud.tencent.com/document/product/1030/31973) 文档。


#### Python SDK 方式
通过 Encrypt 来针对用户的数据进行加密，用于加密的数据大小最多为4KB任意数据，可用于加密数据库密码，RSA Key，或其它较小的敏感信息。本文示例使用腾讯云 Python SDK 实现，您也可以使用其它支持的编程语言。

该 API 操作的 KeyId 和 Plaintext 为必选参数，详情请参见 [Encrypt](https://intl.cloud.tencent.com/document/product/1030/32189) 接口文档来查看其它参数说明。

#### 加密 Python SDK 示例：
通过 KMS 对敏感配置文件`test_encry.dat`进行加密，并将密文传输至服务器进行使用，保证明文数据不落盘。以下示例代码展示了如何使用指定 CMK 对数据进行加密操作。

#### Python 代码示例：
```
# -*- coding: utf-8 -*-
import base64

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
# 导入KMS模块
from tencentcloud.kms.v20190118 import kms_client, models

# 导入可选配置类
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile

def KmsInit(region="ap-guangzhou"):
    SecretId = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    SecretKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

    try:
        cred = credential.Credential(
            SecretId,
            SecretKey)

        # 实例化一个http选项，可选的，没有特殊需求可以跳过。
        httpProfile = HttpProfile()
        httpProfile.reqMethod = "GET"  # GET 请求，默认为 POST
        httpProfile.reqTimeout = 30  # 请求超时时间，单位为秒(默认60秒)
        httpProfile.endpoint = "kms.tencentcloudapi.com"  # 指定接入产品域名(默认就近接入)

        # 实例化一个client选项，可选的，没有特殊需求可以跳过。
        clientProfile = ClientProfile()
        clientProfile.signMethod = "TC3-HMAC-SHA256"  # 指定签名算法
        clientProfile.language = "en-US"
        clientProfile.httpProfile = httpProfile

        # 实例化KMS产品的CLIENT对象
        client = kms_client.KmsClient(cred, region, clientProfile)

        return client
    except TencentCloudSDKException as err:
        print(err)
        return None
def EncryptData(client, keyid, plaintext):
    try:
        #使用CMK加密配置文件
        req = models.EncryptRequest()
        encrypt_params = '''{
            "KeyId" : "%s",
            "Plaintext" : "%s"
            }
        '''%(keyid,bytes.decode(plaintext))
        print(encrypt_params)
        req.from_json_string(encrypt_params)

        #调用加密接口
        encryptResp = client.Encrypt(req)
        #输出加密结果
        print(encryptResp.to_json_string(indent=2))
        #将密文写入文件
        open('test_encry.dat','w').write(encryptResp.CiphertextBlob)
    except TencentCloudSDKException as err:
        print(err)

if __name__ == '__main__':
    client = KmsInit()
    plaintext = base64.b64encode(b'this plaintext for test')
    EncryptData(client,"KeyId", plaintext)
```


### 步骤3：将加密后的数据存储
根据业务的应用场景，将密文进行存储。

### 步骤4：敏感数据解密

#### 控制台方式
详情请参见 [加密解密](https://intl.cloud.tencent.com/document/product/1030/31973) 文档。


#### Python SDK 方式

通过 Decrypt 来针对用户的数据进行解密。本文示例使用腾讯云 Python SDK实现，您也可以使用其它支持的编程语言。

该 API 操作的 CiphertextBlob 为必选参数，详情请参见 [Decrypt](https://intl.cloud.tencent.com/document/product/1030/32198) 接口文档查看其它参数说明。


#### Python 代码示例
```
def DecryptData(client, ciphertext):
    try:
        req = models.DecryptRequest()
        ciphertext_params = '''{
            "CiphertextBlob" : "%s"
            }
        '''%(ciphertext)

        req.from_json_string(ciphertext_params)
        #调用解密接口
        ciphertextResp = client.Decrypt(req)
        #输出解密结果
        print(ciphertextResp.to_json_string(indent=2))
        #输出明文
        print(base64.b64decode(ciphertextResp.Plaintext))

    except TencentCloudSDKException as err:
        print(err)
if __name__ == '__main__':
    #解密配置文件用于程序读取
    ciphertext = open('test_encry.dat', 'r').read()
    DecryptData(client, ciphertext)
```
