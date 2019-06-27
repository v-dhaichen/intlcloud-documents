[Tencent Cloud GME SDK](https://cloud.tencent.com/product/tmg?idx=1)의 사용을 환영합니다. 개발자가 Tencent Cloud GME 제품을 연결하는 데 도움이 되도록 여기에 GME SDK에 적합한 연결 가이드를 소개합니다.

GME 사용에는 다음과 같은 5단계가 있습니다.
1. [Tencent Cloud 콘솔에서 GME 서비스 생성](#.E6.96.B0.E5.BB.BA.E6.9C.8D.E5.8A.A1).
2. [해당 버전의 클라이언트 SDK 다운로드](#.E4.B8.8B.E8.BD.BD-sdk).
3. [API 연결 문서를 참조하여 SDK를 프로젝트로 이송](#.E7.9B.B8.E5.85.B3-sdk-.E6.8A.80.E6.9C.AF.E6.96.87.E6.A1.A3).
4. [일상 운영 백 엔드 통계 보기](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.94.A8.E9.87.8F.E7.BB.9F.E8.AE.A1).
5. [연결 과정 중의 특수한 문제를 자체 해결 및 피드백](#.E7.89.B9.E6.AE.8A.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86).


## 서비스 생성
### 1. 응용프로그램 생성
![](https://main.qcloudimg.com/raw/a4b3dbd8aefd9dd032f8c3ce4154b227.png)

### 2. 해당 정보
해당 페이지에서 필요한 정보를 입력하고 필요에 따라 원하는 서비스를 선택합니다.
- 음질에 따라 비용이 다릅니다. 요금제 세부 정보는 [제품 가격](https://cloud.tencent.com/document/product/607/17808)을 참조하거나 Tencent Cloud 비즈니스 담당 직원에게 문의하시기 바랍니다. 설정 완료 후에 수정할 수 있습니다.
- 게임류 응용프로그램일 경우, 해당하는 플랫폼 엔진을 선택해야 합니다.
- 음성 메시지 및 텍스트 전환 서비스는 설정한 후에 수정할 수 있습니다.

![](https://main.qcloudimg.com/raw/bafdd3250004a5d69322beab1d6c25c7.png)


### 3. 응용프로그램 보기
목록의 AppID는 SDK를 연결하여 개발하는 과정에서 매개변수로 사용됩니다.
![](https://main.qcloudimg.com/raw/9e78b27c75b9bfcd2ce02ae1d02b7046.png)


### 4. 응용프로그램 설정
![](https://main.qcloudimg.com/raw/ac27c53e9a07fa819344f668978fe019.png)
응용프로그램 정보 모듈에서 [수정]을 클릭한 후 해당 정보를 수정할 수 있습니다.

### 5. 인증 정보
![](https://main.qcloudimg.com/raw/76b5038763d2aded0be39b0d1bc27efa.png)
- 이 모듈의 권한 키는 매개변수로 SDK 연결 과정에서 사용됩니다.
- 페이지에서 키를 수정한 후, 15분 ~ 1시간 내에 적용되며 자주 변경하지 않는 것이 좋습니다.
- 게임을 생성한 계정, 기본 계정, 전역 협력자만 [키 리셋]을 조작할 수 있습니다.
- 인증 관련 세부 정보는 [GME 키 설명 문서](https://cloud.tencent.com/document/product/607/12218)를 참조하십시오.
 ![](https://main.qcloudimg.com/raw/df3f92e2eb50aea9d8dde32f252045f6.png)


### 6. 서비스 시작/종료
여기서는 비즈니스 및 서비스의 시작 또는 종료를 진행할 수 있습니다.
![](https://main.qcloudimg.com/raw/a5711820b59c6d4047565562094d1595.png)
![](https://main.qcloudimg.com/raw/ec0f00f1afc229b6db5676772c53edad.png)


## SDK 다운로드
### 1. 다운로드 주소
[SDK 다운로드 가이드](https://cloud.tencent.com/document/product/607/18521)에서 관련 Demo 및 SDK를 다운로드하십시오.

### 2. 연결 준비
SDK 연결은 Tencent Cloud가 제공하는 AppID 및 관련 권한 키를 사용해야 합니다. 즉, 응용프로그램 관리 목록의 AppID와 응용프로그램 설정의 인증 정보 모듈입니다.

플랫폼 관련 구성에 대한 더 자세한 정보는 각 플랫폼 프로젝트 구성 문서를 참조하십시오.

### 3. 공식 Demo 사용 사항
Demo에는 Tencent Cloud 테스트 계정이 있어서 기능 체험을 해볼 수 있습니다. 만일 개인 및 회사용 테스트 계정으로 변경하려면 Demo의 해당 페이지에서 Tencent Cloud 테스트 계정 AppID를 개발자가 콘솔에서 획득한 AppID로 변경하고, AVChatViewController-GetAuthBuffer 함수에서 음성 채팅의 권한 키를 수정해야 합니다.


## 관련 API 문서
사용하는 플랫폼 또는 엔진에 따라 아래 문서를 참조하여 액세스할 수 있습니다.

Unity 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/10783)
[API 문서](https://cloud.tencent.com/document/product/607/15228)

Unreal Engine 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/17025)
[API 문서](https://cloud.tencent.com/document/product/607/15231)

Cocos2D 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/15216)
[API 문서](https://cloud.tencent.com/document/product/607/15218)

Windows 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/19068)
[API 문서](https://cloud.tencent.com/document/product/607/15232)

iOS 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/15219)
[API 문서](https://cloud.tencent.com/document/product/607/15221)

Android 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/15203)
[API 문서](https://cloud.tencent.com/document/product/607/15210)

Mac 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/18617)
[API 문서](https://cloud.tencent.com/document/product/607/18739)

H5 관련 문서:
[프로세스 구성 문서](https://cloud.tencent.com/document/product/607/32156)
[API 문서](https://cloud.tencent.com/document/product/607/32157)



## 콘솔 사용량 통계
[운영 가이드 문서](https://cloud.tencent.com/document/product/607/17448)


## 특수 문제 해결
[FAQ 문서](https://cloud.tencent.com/document/product/607/17359)     [오류 코드 문서](https://cloud.tencent.com/document/product/607/15173)
