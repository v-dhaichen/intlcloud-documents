
本实践指南以 Python 为例，其它语言类似。

## 前期准备

- 依赖环境：Python 2.7 - 3.x版本。
- KMS 产品服务开通：从 [腾讯云控制台](https://console.cloud.tencent.com/kms2) 开通 KMS 产品。
- 云 API 密钥服务开通：获取 SecretID、SecretKey 以及调用地址（endpoint），KMS 的调用地址为 `kms.tencentcloudapi.com`，具体参考各产品说明。
- SDK 安装：执行以下命令，详细可见 [tencentcloud-sdk-python github](https://github.com/TencentCloud/tencentcloud-sdk-python) 开源项目。
```
pip install tencentcloud-sdk-python
```


## 操作流程
您可以通过以下3个步骤完成信封加密场景的操作。
1. 创建主密钥 CMK。
2. 数据信封加密，业务程序通过 API 调用 KMS GenerateDataKey 接口生成数据密钥，系统通过明文密钥将数据加密，并将密文密钥和密文落盘。
3. 数据读取解密，系统读取密文密钥和密文，通过 KMS 解密接口解密密文密钥，返回明文密钥，最后通过明文密钥解密密文数据。


## 实践步骤
### 步骤1：创建主密钥 CMK
主密钥 CMK 的创建指南，请参见 [创建密钥](https://intl.cloud.tencent.com/document/product/1030/32783) 快速入门文档。

### 步骤2：数据信封加密
根据业务需求，在需要新的 DEK 时（例如针对新的用户需要进行加密，或者 DEK 复用超过一定时间，使用新的 DEK 等），可通过 KMS 接口创建新的数据密钥。生成数据密钥后在内存中使用明文密钥加密，最后将密文和密文密钥落盘。

#### 生成数据密钥（KMS Python SDK）

通过 GenerateDataKey 来获取数据密钥 DEK，数据加密密钥是基于 CMK 生成的二级密钥，可用于用户本地数据加密解密。KMS 对 DEK 不做保存管理，需要调用方进行存储。

本文示例使用腾讯云 Python SDK 实现，您也可以使用其它支持的编程语言调用。

该 API 操作的 KeyId 为必选参数，您可以查看 [GenerateDataKey](https://intl.cloud.tencent.com/document/product/1030/32188) 接口文档来查看其它参数说明。

#### Python SDK 示例
```
# -*- coding: utf-8 -*-
import base64,hashlib
from Crypto.Cipher import AES

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

        # 实例化一个 http 选项，可选的，没有特殊需求可以跳过。
        httpProfile = HttpProfile()
        httpProfile.reqMethod = "GET"  # GET 请求，默认为 POST
        httpProfile.reqTimeout = 30  # 请求超时时间，单位为秒(默认60秒)
        httpProfile.endpoint = "kms.tencentcloudapi.com"  # 指定接入产品域名(默认就近接入)

        # 实例化一个 client 选项，可选的，没有特殊需求可以跳过。
        clientProfile = ClientProfile()
        clientProfile.signMethod = "TC3-HMAC-SHA256"  # 指定签名算法
        clientProfile.language = "en-US"
        clientProfile.httpProfile = httpProfile

        # 实例化 KMS 产品的 CLIENT 对象
        client = kms_client.KmsClient(cred, region, clientProfile)

        return client
    except TencentCloudSDKException as err:
        print(err)
        return None

def AddTo16(value):
    while len(value) % 16 != 0:
        value += '\0'
    return str.encode(value)  # 返回bytes

def EncryptData(key,text):
    #初始化加密器
    aes = AES.new(key, AES.MODE_ECB)
    #先进行 aes 加密
    encryptAes = aes.encrypt(AddTo16(text))
    #用 base64 转成字符串形式,执行加密并转码返回bytes
    encrypted_text = str(base64.encodebytes(encryptAes), encoding='utf-8')  
    return encrypted_text

def GenerateDatakey(client,keyid,keyspec='AES_128'):
    try:
        req = models.GenerateDataKeyRequest()
        generatedatakeyParams='''{
            "KeyId" : "%s",
            "KeySpec" : "%s"
        }
        '''%(keyid,keyspec)
        req.from_json_string(generatedatakeyParams)
        #调用生成数据密钥接口
        generatedatakeyResp = client.GenerateDataKey(req)
        #输出加密结果
        print(generatedatakeyResp.to_json_string(indent=2))
        return generatedatakeyResp
        #注，明文密钥需要在内存中使用，密文密钥用于持久化存储

    except TencentCloudSDKException as err:
        print(err)
def Encrypt(key,ciphertext):
    try:
        req = models.EncryptRequest()
        plaintext = open('test_config.conf','r').read()
        entxt = EncryptData(key, plaintext)
        print(entxt)
        #将密文写入文件
        open('test_encode_text.conf', 'w').write(entxt)
        open('test_encode_256.key', 'w').write(ciphertext)
    except TencentCloudSDKException as err:
        print(err)

if __name__ == '__main__':
    #设置创建 KEY 的请求对象
    client = KmsInit()
    generatedatakeyResp = GenerateDatakey(client, 'KeyId', 'AES_256')
	#使用前一步生成的明文数据密钥进行加密
    Encrypt(generatedatakeyResp.Plaintext, generatedatakeyResp.CiphertextBlob)
```


### 步骤3：数据读取解密
先读取落盘的密文密钥，并通过调用解密接口，解密密文密钥。最后根据解密出的明文密钥解密数据。

#### 解密（KMS Python SDK）
通过 Decrypt 来针对用户的数据进行解密。

本文示例使用腾讯云 Python SDK实现，后续您可以使用任何支持的编程语言调用。

该 API 操作的 CiphertextBlob 为必选参数，您可以查看 [Decrypt](https://intl.cloud.tencent.com/document/product/1030/32198) 接口文档来查看其它参数说明。


#### Python SDK 示例
先读取落盘的密文密钥，并通过调用解密接口，解密密文密钥。
```
def Decrypt(cipchertext):
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
        #使用明文解密加密的配置文件
        return base64.b64decode(ciphertextResp.Plaintext)
    except TencentCloudSDKException as err:
        print(err)
def DecryptData(key,text):
    #初始化加密器
    aes = AES.new(key, AES.MODE_ECB)
    #优先逆向解密base64成bytes
    base64Decrypted = base64.decodebytes(text.encode(encoding='utf-8'))
    #执行解密密并转码返回str
    decryptedText = str(aes.decrypt(base64Decrypted),encoding='utf-8').replace('\0','')
    print(decryptedText)
if __name__ == '__main__':
	#解密 DEK
	ciphertext = open('test_encode_256.key', 'r').read()
	decryptData = Decrypt(ciphertext)
	#使用明文密钥解密数据
	DecryptData(decryptData, open('test_encode_text.dat', 'r').read())
```
