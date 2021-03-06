기본적으로 TencentDB for MongoDB는 매일 자동으로 백업합니다. 또한, 사용자가 수동으로 백업할 수도 있습니다.

### 인스턴스 자동 백업

1. 인스턴스는 매일 기본적으로 자동 백업합니다. 자동 백업의 기본 전략은 시작 시간을 01:00 ~ 02:00로 7일 이내 1번의 전량 백업과 6번의 증량 백업을 진행하는 것입니다.
2. 사용자는 자동 백업을 설정할 수 있습니다. 자세한 내용은 다음과 같습니다.
	1. 비즈니스에 쓰기, 업데이트 및 삭제 작업이 빈번하게 수행되는 경우 인스턴스 oplog를 덮어쓸 수 있습니다. 정상적인 백업 및 롤백 작업을 보장하려면 하루에 백업을 여러 번으로 설정할 수 있습니다.
	2. 사용자는 백업 시작 시간을 설정할 수 있습니다. 주의: 매일 백업을 여러 번으로 설정하면 백업 시작 시간은 첫번째 백업 시작 시간입니다.
	3. 백업 이상 여부 알림 옵션을 설정할 수 있습니다. 해당 옵션을 "예"로 설정하면 시스템은 백업 중에 oplog를 덮어쓰는 것을 발견하면 알람 수신자에게 이벤트 알람을 전송합니다. 특정 경보 구성에 대해서는 제품 이벤트 목록의 CM 이벤트 경보 및 설정을 참조하십시오.
	![](https://main.qcloudimg.com/raw/97c3b30b015845c2de6fe8accca12cad.png)
3. 백업 리스트는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/7c6a48c59d8f1a88f4bbc956351ca03f.png)

### 인스턴스 수동 백업
인스턴스 세부 정보 페이지에서 수동 백업을 클릭하고 비고 정보를 입력한 후, 백업 작업을 수동으로 제출할 수 있습니다. 백 엔드 관리 시스템이 해당 작업을 실행합니다.
![](https://main.qcloudimg.com/raw/b67a177016b10d3d27597d914e35f51d.png)

