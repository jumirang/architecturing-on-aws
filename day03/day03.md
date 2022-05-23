* VPC 엔드포인트
  * Gateway 엔드포인트 : 가상 라우터
    * IGW처럼 VPC 경계에 위치
    * VPC내 EC2 Private Subnet의 RT상 vpce 추가 필요
    * VPC외 S3, DDB only
    * 추가 비용없이 무료로 사용
  * Interface 엔드포인트 : ENI
    * VPC내 EC2 Private Subnet안에 위치
    * VPC외 SQS, CloudWatch 등.. 서비스와 Private Link로 연결
    * 가격, 비용이 있음

* VPC 피어링
  * Multi-VPC
  * 서로 다른 VPC상 개발, QA, PROD 형상 존재시 서로 통신이 필요

* Route 53
  * DNS 서비스 (도메인 이름을 IP 주소로 변환)
  * DNS 상태체크 (리전별 LB가 정상인지 체크)
  * 리전별 고가용성 제공
  * 지리적 위치 라우팅 (미국 사용자는 미국리전, 유럽 사용자느 유럽리전 LB로 라우팅)
    * 디폴트 규칙 설정 가능
  * Route 53 Resolver

* 서버리스
  * API Gateway
    * HTTP, Rest, Websocket(양방향 통신 ex. 실시간 채팅상담)
    * AWS WAF와 함꼐 사용 (DDoS 보호)
  * SQS
    * 완전관리형 메시지 대기열 서비스
    * WEB --- SQS --- WAS로 구성하여, 고가용성 비동기 처리
    * 오토 스케일링
      * SQS 대기열 등록 메세지 수량을 CW 지표로 등록 후, 경보 발생하여 처리
    * 표준, FIFO 유형
      * FIFO : 정확한 순서대로 처리 서비스 (ex. 수강신청, 기차표예매, 가격변화추이). 성능제약 (초당 300개 API, 높은처리량 3000 API)
  * SNS
    * 주제(topic)
      * 표준 : 이메일, 문자, 모바일앱
      * FIFO : SQS (최대 100명 구독자 가능)
  * Kinesis
    * Video Streams: 라이브 비디오, 저장
    * Data Analystics : 스트리밍 데이터 필터링, 변환 후 분석
    * Data Streams : 실시간으로 데이터 수집 및 저장
    * Data Firehose : 준실시간으로 데이터 처리 및 분석 도구에 전송
  * Step Functions
    * 서비리스 형태로 여러 서비스 이용할 시 어떤 순서대로 데이터를 처리할 지 "work flow"를 정의해서 서비스를 구현
    * 일종의 상태 머신 : 출력을 결정하기 위해서 일련의 작동 조건을 의존하는 객체
    * States Language
    * 워크플로우를 시각적으로 구축, 모니터링, 수동작업(중지, 시작)

* 엣지 서비스
  * AWS 리전밖에서 제공되는 서비스
  * 엣지 로케이션
    * CDN POP Site에 대한 AWS 표현
      * Content Delivery Network
  * CloudFront
    * CloudFront 배포하면 cloudfront.net 도메인 제공
    * 오리진 설정 (S3, LB, EC2 등)
    * 동적 콘텐츠, 정적 콘텐츠별 나눠 구성
      * 동적 콘텐츠 : 시간이 지나면 변경되는 컨텐츠, input에 따라 output 다름
        * TTL=0 설정하여 항상 오리진으로 요청
        * 항상 오리진 요청 (LB). 왜 CloudFront 사용?
          * CloudFront 가속화 기능 : AWS 글로벌 백본 네트워크 사용, gzip 압축 지원
      * 정적 콘텐츠 : jpg, mov, text
        * TTL=3600 설정하여 CloudFront 캐싱
  * Global Accelerator 솔루션
    * 어플리케이션 속도 및 가용성 높임
    * 애니캐스트 IP
  * AWS WAF
    * 웹방화벽 : HTTP Header로 트래픽 허용, 차단
      * 웹 ACL을 만들고 규칙 추가
        * IP, 규칙 그룹
    * 기존 방화벽 : TCP/UDP port, IP로 트래픽 허용, 차단
    
* 재해 복구
  * AWS Backup : 중앙 집중식 관리

* 도움 링크
  * https://github.com/serithemage/AWSCertifiedSolutionsArchitectUnofficialStudyGuide
  * AWS 자격증 가이드 : https://amz.run/5Zw6
  * AWS 디지털 트레이닝 플랫폼 가이드 : https://amz.run/5Zw8
  * AWS 무료 디지털 과정 리스트 : https://amz.run/5Zw9
  * ARCH 과정 LAB 레코딩 사이트 : https://bit.ly/arclabv7 
