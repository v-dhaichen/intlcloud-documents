## 计费方式

数据万象按照**实际使用量付费**，采用**后付费**方式，次月3 - 7日会出本月账单，进行账号扣费。

由于数据万象的存储是基于 COS，所以存储部分的费用会在对象存储服务（COS）的账单中给出。具体费用可参考 [COS 产品定价](https://intl.cloud.tencent.com/document/product/436/6239)。


## 计费冻结机制
本月结算完成后，将以本月账单金额的120%对帐户进行下月费用预估冻结。下月结算时，先解冻上月的冻结费用，再进行本月使用额度的扣费。


<span id="计费项说明"></span>
## 计费项说明
数据万象 CI 计费项包括：**基础图片处理费用和**流量费用**。下面是各计费项的解释说明及定价详情。


### 基础图片处理费用

基础图片处理费用指用户在下载或做持久化操作时，对图片进行处理所产生的费用，具体功能请参见 [功能介绍](https://intl.cloud.tencent.com/document/product/1045/33424)。

- 基础图片处理费用采用按量计费方式，计费周期为**月**。
- 基础图片处理功能按照图片原文件大小进行数据处理量计算，如原图为4MB大小进行转码处理，则按照4MB进行计量。
- 基础图片处理定价为**0.01USD/GB**。

### 流量费用

流量费用包括 **CDN 回源流量**和**外网出流量**两部分，当前数据万象不对入流量收取费用。流量费用按照阶梯累进计费，具体说明和定价参见下表。
- 入流量：数据上传至数据万象产生的流量。
- CDN 回源流量：通过腾讯云 CDN 访问数据万象，CDN 回源产生的流量。
- 外网出流量：直接通过数据万象域名链接访问所产生的流量。

**中国大陆地域**

<table>
   <tr>
         <th colspan=1 rowspan=2><center>地域</center></th>
     <th colspan=3><center>流量费用（USD/GB）</center></th>
   </tr>
   <tr>
      <th>入流量</th>
      <th>CDN 回源流量</th>
      <th>外网出流量</th>
   </tr>
   <tr>
      <td>北京、上海、广州、南京、重庆、成都</td>
      <td>免费</td>
      <td>0.02</td>
      <td>0.1</td>
   </tr>
</table>

**中国香港及境外地域**


<table>
   <tr>
	 <th colspan=1 rowspan=2><center>地域</center></th>
     <th colspan=3><center>流量费用（USD/GB）</center></th>
   </tr>
   <tr>
      <th>入流量</th>
      <th>CDN 回源流量</th>
      <th>外网出流量</th>
   </tr>
   <tr>
      <td>新加坡</td>
      <td>免费</td>
      <td>0.072</td>
      <td>0.072</td>
   </tr>
      <tr>
      <td>加拿大多伦多</td>
      <td>免费</td>
      <td>0.07</td>
      <td>0.07</td>
   </tr>
      <tr>
      <td>俄罗斯莫斯科</td>
      <td>免费</td>
      <td>0.07</td>
      <td>0.07</td>
   </tr>
      <tr>
      <td>印度孟买</td>
      <td>免费</td>
      <td>0.1</td>
      <td>0.1</td>
   </tr>
      <tr>
      <td>中国香港</td>
      <td>免费</td>
      <td>0.08</td>
      <td>0.08</td>
   </tr>
</table>


>通过 CDN 下发到用户终端产生的流量不在数据万象计费范畴，按 CDN 计费标准收取，详见 [CDN 计费](https://intl.cloud.tencent.com/document/product/228/2949)。


