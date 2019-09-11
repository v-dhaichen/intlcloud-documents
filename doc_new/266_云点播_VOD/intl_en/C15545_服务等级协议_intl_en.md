**In order to use the Tencent Cloud Video on Demand ("VOD") service (the "Service"), you should read and observe this Video on Demand Service Level Agreement (this "Agreement", or this "SLA") and the [Tencent Cloud Service Agreement ](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, *among others*, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1.  Terms and Definitions
1.1  **Tencent Cloud Video on Demand (VOD) Service**: means the one-stop VPaaS service provided by Tencent Cloud to you, which integrates audio and video storage management, audio and video transcoding and audio and video speed-up playing, with the billing mode of pay per storage, transcoding or traffic usage. For details, please refer to the Service you purchase, and the contents of the Service provided by Tencent Cloud.
    
1.2  **Error Rate**: Error Rate = (the number of "5xx" errors within unit time + the number of requests made by a user in a regular way that fail to reach the VOD server due to Service malfunction within unit time) / the number of all requests made by a user within unit time.

> 5xx: HTTP status code indicating server errors.

1.3  **Service Unavailability**: If the Error Rate of the Service is higher than 0.05% (exclusive) within one unit time (each five (5) minutes as one calculation time unit), it shall be deemed that the Service is unavailable within such unit time; when such situation lasts for ten (10) minutes or more, such time shall be counted into the Service Downtime, while any such situation that lasts less than ten (10) minutes will not be counted into the Service Downtime.

1.4  **Service Downtime**: means the aggregate time of Service Unavailability calculated in minutes within a Service Month.

1.5  **Service Month(s)**: means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.

1.6  **Significant Impromptu Increase of Business Scale**: The Service is not subject to any storage, transcoding or traffic limitations, and is scalable on a dynamic basis to meet your actual business needs; *provided, however*, that you should notify Tencent Cloud at least 3 business days in advance in writing in case of any significant impromptu increase of business scale, otherwise the availability of the Service may be affected. Tencent Cloud does not make any guarantee to the availability of the Service in case of any significant impromptu increase of business scale that you fail to so notify Tencent Cloud, nor will Tencent Cloud be liable for any impact on the availability of the Service thereof.

**Impromptu Increase Metrics**:

- bandwidth: peak requests expected to increase by more than 50Gbps, or peak requests increased by more than 10Gbps with significant concentration in terms of territory and operator.
- storage: the volume of storage expected to increase by more than 100TB.
- transcoding: the output of transcoding expected to increase by more than 100,000 minutes/day.
- video content audit: the length of video content to be audited expected to increase by more than 40,000 minutes/day 

## 2.  Service Availability/ Service Uptime Metrics

2.1	**Calculation of Service Availability**

**Service Availability = (1 – Service Downtime / total time within a Service Month) × 100%**

2.2	**Standard of Service Availability/ Service Metrics**

**The Service Availability of the Service provided by Tencent Cloud will be no less than 99.7%.** You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. 


## 3.  Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

3.1  **Standards of Compensation**

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud's official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service (Tencent Cloud VOD service) by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable monthly service fee paid by you for such month** (the monthly service fee referred to herein shall exclude the portion deducted by a voucher or promotional credit, due to discounted service fee or otherwise deducted).

|**Service Availability (Av) for a Service Month** |  **Value of Compensation Voucher**|
|---------------------------------------------------| --------------------------------------------------------|
|99.7% > Av ≥ 99%	|10% of the monthly service fee for the applicable month|
|99% > Av ≥ 95%	|25% of the monthly service fee for the applicable month|
|95% > Av|	50% of the monthly service fee for the applicable month|

3.2  **Time Limit for Compensation Application**

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the third (3^rd^) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4.  Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1	any system maintenance with prior notice by Tencent Cloud to you, including system cutover, maintenance, upgrade and malfunction simulation test.

4.2	any malfunction or configuration adjustment of any network or equipment that is not Tencent Cloud facility.

4.3	any attack on any of your application endpoints or data, or any other mal-operation.

4.4	any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures.

4.5	any negligence in authorization or mal-operation by you, or any of your equipment, or third-party software or device.

4.6	any failure of you to abide by user guide or suggestions for using Tencent Cloud products.

4.7	any malfunction due to block of a domain name caused by your illegal or prohibited content or otherwise.

4.8	any decline in the availability of the Service due to your impromptu increase of traffic without prior written notice to Tencent Cloud.

4.9	any Service Unavailability or failure of the Service to meet the availability standard due to any reason not attributable to Tencent Cloud.

4.10	any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.


## 5.  Miscellaneous

5.1 **The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course and will announce such amendment via a notice on its website, an email notice or a text message notice. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended, and no additional consent is required from you therefor.

5.3 As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)
