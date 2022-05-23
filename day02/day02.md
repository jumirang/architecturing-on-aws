* Amazon S3
  * 객체 스토리지 솔루션
  * 비용 절감
  * 보안 강화
  * 사용 사례
    * 백업 및 복원
      * Data Lake : table, csv, text .. 정형, 비정형 데이터를 가지고 머신러닝 같은데 분석 용도로 사용
    * 비즈니스 크리티컬 어플리케이션 : 정적 데이터
    * 아카이빙 및 규정 준수 : compliance 체크 가능
  * S3 특징
    * 데이터는 여러 AZ에 중복 저장
    * 최대 5TB의 파일을 S3에 저장
    * S3 버킷에 무제한의 데이터 저장
  * 버킷 정책과 IAM 정책을 쉽게 만들 수 있는 사이트 
    * https://awspolicygen.s3.amazonaws.com/policygen.html
  * S3 스토리지 클래스
    * 비디오(TV, 영화)
      * 최신 : 액세스 빈도 high
      * 시간이 지나면 액세스 빈도 low
    * 고빈도 : S3 Standard (default)
    * 저빈도 : S3 Standard-IA (여러 AZ), S3 One Zone-IA (하나 AZ. 비용 낮음)
    * 저저빈도 : 데이터 아키이브용 S3 Glacier (장기보관목적)
    * S3 Intelligent-Tiering : 연속 30일 이상 엑세스 없으면, 자동으로 S3 Standard-IA으로 변경해 줌
  * 사용 사례
    * 한번 쓰고 여러번 읽어야 하는 경우 (웹 호스팅)
    * 사용자가 매우많고 콘텐츠 양이 다양함

* 공유 파일 시스템
  * 여러 인스턴스가 동일한 스토리지를 사용해야 하는 경우?
    * EBS는 하나의 인스턴스에 하나의 스토리지로 사용
    * EFS, FSx 사용 필요
  * Amazon FSx
    * Multi-AZ 지원하지 않아 백업을 위해 S3 연동

* 데이터 마이그레이션 도구
  * 오프라인
    * AWS Snowball
  * 온라인
    * AWS Storage Gateway
      * 온프레미스 상 어플리케이션 서비스에서 AWS S3을 연동해서 제공시 문제(보안, 지연) 해결 목적
      * 온프레미스 어플리케이션 <-- AWS Storage GW --> AWS S3
    * DataSync
      * 온프레미스에 있는 Block, 파일을 비동기적으로 AWS S3, EFS와 sync 시켜줌
    * AWS Transter Family : SFTP서버를 통해 S3로 배포

* 데이터베이스
  * Amazon EC2에서 데이터베이스 책임 : 고객이 OS패치, 데이터베이스SW패치/백업, 고가용성, 스케일링, 앱최적화를 관리해야 함
  * AWS 관리형 데이터베이스 서비스는 고객은 앱최적화만 관리하고, 나머지는 AWS가 관리(단, 고객이 정책은 수립해야 함)
  * 관계형 데이터베이스 : RDS, Redshift, Aurora
    * 스키마 고정
    * 과도한 읽기/쓰기 용량을 필요하지 않음 : 하나의 서버에서만 처리 (다중AZ 이긴하나, 하나 서버만 사용)
    * 최상의 성능을 필요로 하지 않음
    * 수직 스케일링 : 하나의 데이터베이스 서버로 CPU, Memory 증감으로 스케일링
  * 비관계형 데이터베이스 : DynamoDB, ElasticCache
    * 스키마 동적
    * 수평 스케일링 : 데이터베이스 서버 개수를 수평으로 증감

* DynamoDB Accelerator
  * 어플리케이션 -- DAX -- DynamoDB : DAX 캐쉬를 두어 밀리초 이하의 dynamodb 성능을 제공 가능
* 데이터베이스 마이그레이션 서비스

* 모니터링
  * 운영상태
  * 어플리케이션 성능
  * 리소스 사용률
  * 보안 감사
  * 비용 모니터링 필요
    * AWS Cost Explorer : AWS 리소스 비용을 추적, 예측 (서비스, 태그 기반)
    * AWS Budgets : 실시간 비용 모니터링 (기준치 초과시 알림)
  * 로그 유형
    * CloudWatch Logs
      * access log상 500 에러를 지표로 등록하여, CW 경보로 등록하여 SNS 연동
    * CloudTrail
      * 보안적인 개념의 모니터링
      * AWS 계정 기반의 활동을 로깅하고 모니터링 함. AWS 서비스가 API call 기반이라 (ex. 누가 인스턴스를 종료했는가?)
    * VPC Flow Logs
      * tcpdump의 aws 버전

* 자동화
  * 고가용성, 탄력성을 갖춘 인프라를 구축하고 엔드유저에게 서비스 제공
  * 수동 -> 자동으로 리소스 배포 필요
  * 코드형 인프라(IaC) 도입 필요
  * AWS Elastic Beanstalk
    * 호스트, OS ~ HTTP 서버까지 AWS에서 관리 (VPC, Subnet, 스케일링, ELB, 자체도메인 제공)
    * 사용자는 코드만 관리하면 됨
  * CloudFormation
    * Drift 감지기능 : 인프라에 자동화 배포된 내용과 현재 내용과 비교해서 수동으로 작업한 내용을 찾아낼 수 있다
  * AWS 솔루션 구현
    * 산업별, 기술별로 어떤 서비스 배포할 수 있는지
    * 배포 스크립트와 CF템플릿을 AWS 솔루션에 등록해서, 서비스 배포
  * AWS CDK(Cloud Development Kit)
    * AWS CDK앱 소스코드 -> 템플릿 -> CloudFormation -> 스택
  * System Manager
    * 운영 관리
    * 어플리케이션 관리
      * Parameter Store : 어플리케이션에서 사용할 파라미터 값을 저장하여 사용
      * AWS AppConfig : 환경별 configuration을 통합적으로 관리
    * 작업 및 변경
    * 인스턴스 및 노드
      * 세션 관리자 : 원격 접속 (Key없이 원격접속 가능)
      * Run Command : Document에 명령어 정의 후, 수행하여 EC2 제어
      * 상태 관리자

* 컨테이너
  * 도입 목적 : 마이크로서비스와 컨테이너
  * 마이크로서비스 : 독립적으로 각 서비스 어플리케이션을 개발,운영 관리
  * 컨테이너 : 코드, 구성, 종속성, 라이브러리를 하나의 이미지로 패키징한 것
    * LINUX - Docker - Containers
  * 하나의 EC2 위에 여러 컨테이너를 띄워 운영할 수 있다 (부팅속도도 VM대비 빠름)
  * 컨테이너 관리도구 Docker 필요
  * AWS 관련 서비스
    * Amazon ECS
      * 손쉽게 컨테이너를 배포, 사용
      * AWS 서비스 이용 (VPC, Subnet, EC2, ELB, Auto scaling)
      * 앱정의(task definition) : ECR에 저장된 이미지, 컨테이너가 필요한 CPU, Memory 용량 정의
      * ECS 클러스터
      * 컨테이너 = task
    * Amazon EKS
      * 클러스터 프로비저닝 : Control Plane(Kube관리)과 Data Plane(node, pod(컨테이너)) 생성
      * Control Plane을 AWS 관리형으로 관리
      * Data Plane은 고객들이 관리해야 함
    * AWS Fargate
      * 컨테이너를 serverless로 배포
      * Fargate / ECS : 고려 사항
        * https://docs.aws.amazon.com/ko_kr/AmazonECS/latest/developerguide/AWS_Fargate.html#fargate-task-defs

* 퀴즈
  * Auto Scaling : DDB, EC2, RDS 스토리지
    * RDS 스토리지 auto-scaling이 어떤 방식으로 되는 것인지요? (RDS 스케일 업은 매뉴얼로 하는 것으로 알고 있는데, 워크로드 발생시 자동으로 스케일링 되는 게 어떤것인지)
      * Aurora 만 해당?
    * DDB, EC2는 scale-out 형태로 스케일링
  
* 질문
  * 보안그룹의 소스를 CIDR IP대역이 아닌 다른 보안그룹으로도 지정이 가능한데 동작 원리가 궁금합니다.
    * Ans) WS(EC2 보안그룹A) -> WAS(EC2 보안그룹B) : 보안그룹B 소스에 보안그룹A를 지정하면, WS에서 요청시 WAS의 보안그룹 상 보안그룹A는 WS의 사설IP 기반으로 연동됨
    * https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_SecurityGroups.html#SecurityGroupRules
  * DynamoDB도 수밀리초 내 응답을 제공해주는데, DAX 캐쉬를 두어서 쓰는 이유가 응답속도를 수밀리초에서 줄이는 것 말고 어떤 이점이 있어서 사용하면 좋을지요? (예로 DynamoDB도 스캔동작 시 조회할 데이터가 많으면 전체 조회시간이 꽤 늘어나는데, 이런 스캔동작 시간이 획기적으로 줄어든다던가 하는 조회동작의 차이가 있을지)
