**In order to use the Tencent Cloud Elastic MapReduce ("EMR") service (the "Service"), you should read and observe this Elastic MapReduce Service Level Agreement (this "Agreement", or this "SLA") and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, *among others*, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1.  Terms and Definitions

1.1  **Elastic MapReduce (EMR)**: means services provided by Tencent Cloud including Hadoop cluster creation, Hadoop installation and deployment, elastically scalable clusters, computing and storage engines, and monitoring, operation and maintenance support. For details, please refer to the Service you purchase and the contents of the Service provided by Tencent Cloud.

1.2  **Unit Time**: For measuring the Service, each 5 minutes will be deemed as one measurement unit, resulting in 288 measurement points each day. The measurement point of 00:00:00 represents the time slot from 00:00:00 to 00:04:59, and the rest can be deduced by analogy.

1.3  **Error Rate within Unit Time**: means the percentage of the number of failed requests within Unit Time due to any reason attributable to Tencent Cloud out of the total number of valid requests within Unit Time Error Rate within Unit Time = the number of failed requests within Unit Time / the total number of valid requests within Unit Time. Failed requests refer to valid requests with HTTP returned error code of 500 (Internal Error) or 503 (Service Unavailable). Valid requests refer to the calling of any function of the Service via [API](https://cloud.tencent.com/document/product/589/10215), excluding any traffic restriction requests due to the triggering of frequency control and any failed requests due to the upgrade, alteration or shutdown of the Service. Any request of Service via API from a user due to hacker attack shall not be deemed as a valid request.

1.4  **Service Unavailability**: The Service unavailability will be calculated based on the Error Rate within Unit Time, excluding any circumstance as provided for in the release of liabilities provisions below. If you do not make any request within a Unit Time, it will be deemed that the Service is 100% available within such Unit Time.

1.5 **Service Month(s)**: means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.

1.6  **Monthly Service Fee**: Monthly Service Fee will be calculated based on the use of clusters (i.e., elastic MapReduce clusters) of the Service per Service Month.



## 2.  Service Availability

2.1   **Calculation of Service Availability**

Error Rate within Unit Time = the number of failed requests within Unit Time / the total number of valid requests within Unit Time

Service Availability = 1 -- (the sum of the Error Rate within Unit Time within a Service Month / the total number of Unit Time measurement units within a Service Month) × 100%

2.2  **Standard of Service Availability / Service Metrics**

**The Service Availability for the Service provided by Tencent Cloud will be** **no less than 99.9%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below.

3.  **Service Compensation**

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

## 3.  Standards of Compensation

(1) Compensations will be made **in the form of coupon** by Tencent Cloud, and you should follow the rules for using the coupon (including the valid term; for details, please refer to the rules of coupons published on Tencent Cloud's official website). You cannot redeem such coupon for cash or request to issue an invoice for such coupon. Such coupon can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the coupon to purchase other services of Tencent Cloud, nor should you give the coupon to a third party for consideration or for free.

(2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by a coupon or promotional voucher, due to discounted service fee or otherwise deducted).

|**Service Availability (Av) for a Service Month**  | **Value of Compensation Coupon**|
|--------------------------------------------------- |----------------------------------|
|99.9% > Av ≥ 99%|	10% of the Monthly Service Fee |
|99% > Av ≥ 95%|	20% of the Monthly Service Fee |
|95% > Av	|100% of the Monthly Service Fee |


3.2 **Time Limit for Compensation Application**

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5^th^) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

3.3 **Application Materials for Compensation**

If you believe that the Service fails to meet the Service Availability standard specified herein, you may apply for compensation within the period of time as stipulated under this SLA, and you should at least provide the following information together with your compensation application:

(1) your account information, including your account ID and APP ID.

(2) explanation of the grounds for the application, specifying the Service Availability calculated by you and the calculation method, and details of each failed request (including the initiation time of the request, the interface name of the request and the return value).

(3) any other information reasonably required by Tencent Cloud.


## 4.  **Release of Liabilities**

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1	any malfunction attributable to user mode, including without limitation improper configuration parameters, unreasonable use of resources, and business logic bug.
4.2	any malfunction due to any device, software or other technology of you or any third party (other than any third party directly controlled by the Service).
4.3	any malfunction on user mode due to any bug within the scope of open source community components.
4.4	any malfunction attributable to you or any third-party collaborator (such as CVM resource restriction, COS capacity restriction, CAM role, security group, and VPC configuration).
4.5	any Service Unavailability or failure of the Service to meet the availability standard due to any reason not attributable to Tencent Cloud.
4.6	any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.


## 5.  **Miscellaneous**

5.1	The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.
5.2	Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.
5.3	As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

