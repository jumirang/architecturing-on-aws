* 고객이 AWS로 이전하는 이유
  * 민첩성 증가
    * 출시 기간 단축 : 비즈니스의 속도, 민첩성 개선
    * 원활한 스케일링 : 동적인 워크로드 변화
  * 복잡성 및 위험 감소
    * 비용 최적화 : 다양한 요금옵션, 최적화 서비스
* 서비스 엔드포인트 및 할당량
  * https://docs.aws.amazon.com/ko_kr/general/latest/gr/aws-service-information.html

* 가용 영역(AZ) // = 하나 이상의 데이터 센터(DC) 구성 그룹 (EC2, RDS, EBS ..)
  * 고가용성 달성에 사용됨 : aws 리소스들은 여러 AZ에 걸쳐서 배포
  * 배포 수준
    * AZ에 배포 : EC2, RDS, .. (생성시 AZ 하나를 선택) // 사용자가 여러 AZ 구성필요
    * 리전에 배포 : S3, DDB (생성시 AZ 선택안함) // aws가 여러 AZ 데이터를 중복 저장
  * AZ간에 Private Link로 연결됨

* 리전
  * AZ 2개 이상으로 구성
  * 리전간에 AWS 글로벌 인프라로 연결됨

* 리전 선택에 영향을 미치는 요인
  * (중요) 거버넌스 : 보안, 규정 준수
    * 서비스 제공 데이터를 대한민국에서만 -> 서울 리전 선택
  * 지연 시간 : 지연시간과 서비스 만족도가 연관 (ex. 게임) -> end-user와 가까운 리전 선택
  * 서비스 가용성
    * AWS Re:Invent 신규서비스 기능 발표 (처음부터 모든리전에 서비스 X) -> 요구가 있는 리전부터 개시

* IAM
  * IAM 정책 : IAM 사용자, 사용자 그룹, 역할에 권한 부여

* AWS Organization
  * 다중 계정 : 통합 결제, 서비스 제어 정책(여러 AWS 계정에게 access 제어)

* AWS Well-Architected Tool
  * self 서비스 형태로 분석
  * 도메인별 렌즈(= 지침)
    * SAP, 서버리스, 스트리밍, IoT .. 각 별도의 지침 제공
  * Well-Architected Framework Main page
    * https://aws.amazon.com/ko/architecture/well-architected/

* 공유 및 전용 테넌시
  * Hypervisor ( HW | OS | Hypervisor | VM(App, OS) 계층 구조 )
    * VM의 시작, 중지 제어
    * H/W 리소스 관리 (공유)
    * 보안
    * 고가용성
  * EC2 디폴트로 공유 테넌시 (위 hypervisor 개념 적용)

* 인스턴스 스토어 볼륨
  * EC2와 볼륨이 local로 연결되어 있어, 네트워크로 연결된 EBS 보다 더 빠르게 구성할 수 있다
  * EC2 중지 시 인스턴스 스토어 볼륨 삭제될 수 있음 (휘발성)
