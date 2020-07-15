# 아마존 웹 서비스 (AWS)
## 왜 AWS를 사용해야 하는가?


## Amazon Server
### Amazon EC2 : 가상 서버 서비스
 + virtual Machine
 
 + 재구성이 가능한 컴퓨팅 리소스
 
 + 쉽게 확장/축소되는 컴퓨팅 용량
 
 + 고객 업무 영역에 따른 다양한 인스턴스 타입 제공
 
 + 사용한 만큼만 과금
 
 ***
 
 ## Amazon Storage
  ### Amazon S3
   + 객체 기반의 무제한 파일 저장스토리지
   + URL를 통해 파일 공유가능
   + 99.99%의 내구성
   + 사용한 만큼만 지불 (GB당 과금)
   + 정적 웹 사이트 호스팅 가능
   + 많은 서버와 통합해서 사용가능
   + 개발소스와 배포는 s3를 통해서 가능
   + 라이프사이클관리를 통해서 30일 이상지난 데이터를 Amazon IA로 백업하고 또 30일 지나면 Amazon Glacier에 데이터백업
   + 1TB당 소요되는 비용은 S3 = 25$ IA = 18$ glacier = 5$
   
  ### Amazon Glacier : 아카이빙/백업 스토리지
   + 99.9999%의 내구성 
   + 백업 / 아카이빙 용도의 cold데이터
   + 사용한 만큼 낮은 비용으로 활용 가능
   
  ### Amazon EBS : 블록스토리지
   + EC2에 attach해서 쓸 수 있는 스토리지
   + 단일 가용 영역내에서 여러 서버에 걸쳐 복제
   + 특성 시점에 대한 볼륨 스냅샷을 만들 수 있는 기능제공
   + S3에 저장되어 복수의 가용영역에 걸쳐 자동으로 복제
   + 파일을 생성하는것도 과금이 들어감
  
  ### Amazon CloudFront : 콘텐츠 전송 네트워크
   + 컨텐츠를 캐싱하여 성능 가속
   + 전세계 216개 엣지 로케이션
   + AWS 서비스 -> CloudFront 간 데이터 전송 무료
   + 글로벌 고속 백본 네트워크 확보
   + DDos 방어 무료 제공
   
 ***
   
  ## Amazon Databases
  ### Amazon RDS : Managed 관계형 데이터베이스 서비스
   + 완전 관리형 관계형 DB서비스
   + 다양한 DB 엔진 제공 (PostgerSQL, Aurora, MYSQL...)
   + DB 이중화
   + Read Replica
   + 인스턴스 확장
   
  ### Amazon Aurora
   + 호환성 (Mysql 5.6 완벽호환/ PostgreSQL 9.6 완벽호환)
   + 성능향상 (기존 Mysql 대비 5배 / PostgreSQL 대비 3배)
   + 고가용성 및 내구성
   + 상용 DB엔진 대비 1/10 가격
   + 가장 빠르게 성장하는 AWS 서비스
   
  ### Amazon DynamoDB : 관리형 no SQL 데이터베이스
   + 빠르고 일관된 서능
   + 뛰어난 확장성 (Auto scailing)
   + 완전 관리형
   + 이벤트 주도 프로그래밍 (Lamda에서 이벤트가 발생했을때 데이터저장가능)
   + 세분화된 액세스 제어 (타입별로 세분화시켜서 데이터 저장가능)
   + 유연성
   + 데이터베이스에서 조금 느린 지연시간
   
  ### Amazon ElastiCache
   + 탁월한 성능
   + 완전 관리형
   + 확장성
   + 엔진은 두가지
     + Redis용 Amazon ElastiCache
     + Memcached 용 Amazon ElastiCache
   + **memcache는 로그인세션 정보를 가지고 있어서 LoadBalancer 가 서버전환을 하더라도 로그인정보**
