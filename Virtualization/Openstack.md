# 오픈스택(OpenStack)
## 오픈스택이란?
 + IaaS 형태의 클라우드 컴퓨팅 오픈 소스 프로젝트
 + 2012년 창설된 비영리 단체인 OpenStack Foundation에서 유지, 보수하고 있으며 아파치 라이선스하에 배포
 + 클라우드 컴퓨팅을 위한 오픈소스 소프트웨어 플랫폼
 + 클라우드 서비스를 배포하는 소프트웨어
 + 프로세싱, 저장공간, 네트워킹의 가용자원을 제어하는 목적의 여러 개의 하위 프로젝트로 이루어짐

***

## 오픈스택 버전

 ### 1) compute (프로젝트: Nova)
  + 주요 모듈은 파이썬으로 구현
  + 인스턴스(가상머신, 서버)의 생성, 중지, 스케쥴링 등 인스턴스의 라이프사이클을 관리
  + KVM, Xen, VMware 등 하이퍼바이저 기술 사용
  + 오픈스택에서 CPU, Memory 등을 제공
  + OpenStack Compute에서는 인증은 OpenStack Identity를 통해, 디스크와 서버 이미지는 OpenStack Image 서비스를 통해, 사용자와 관리자 인터페이스는 OpenStack 대시보드를 통하여 상호작용
  
 ### 2) Identity (프로젝트: Keystone)
  + 모든 컴포넌트의 인증을 담당
  + LDAP과 같은 기술을 사용하여 사용자의 중앙 디렉토리 기능을 함
  + 각 서비스의 주소와 토큰을 관리
  + 
  
 ### 3) Image (프로젝트: Glance)
  + 인스턴스를 생성하기 위한 운영체제 디스크 이미지를 제공 (Qcow2, Ova)
  + 디스크나 서버 이미지에 대한 API 요청과 최종 사용자와 OpenStack Compute 구성 요소로부터의 메타데이터 정의를 허용
  + OpenStack 오브젝트 스토리지를 포함한 다양한 스토리지 타입에서 디스크나 서버 이미지 저장을 지원
 
 ### 4) Object Storage (프로젝트: Swift)
  + 사용자가 사용 할 수 있는 클라우드 스토리지
  + Http 기반의 RESTful API를 제공
  + 수평 확장 가능한 분산 스토리지
  + 복사본을 구성하여 안전한 대용량 스토리지
  
 ### 5) Orchestration (프로젝트: Heat)
  + 탬플릿 기반으로 다양한 클라우드 어플리케이션을 배치 및 관리 할 수 있는 오케스트레이션 기능제공
  + OpenStack 서비스들과 관련한 측정 데이터를 효율적으로 수집
 
 ### 6) Telemetry (프로젝트: Ceilometer)
  + 오픈스택 전체 환경을 에이전트 기반으로 데이터 수집
  + 수집한 데이터로 모니터링, 사용량, 벤치마킹, 확장성, 통계 등을 제공하는 서비스
  + 서비스들로부터 발송된 notification을 모니터링하여 이벤트와 측정 데이터를 수집
  + 데이터 저장소와 메시지 큐를 포함한 다양한 목적지에 수집한 데이터를 발행
  
 ### 7) Volume (프로젝트: Cinder)
  + 인스턴스의 영구 저장장치인 블록장치를 제공
  + 블록 스토리지 장치를 생성, 관리 할 수 있도록 플러그인 가능한 드라이버 아키텍처 구조
  + **LVM, Red Hat Ceph, Red Hat GlusterFS, EMC, NetApp, IBM GPFS, HP storeVirtual, Nexnta 등 스토리지 지원**
 
 ### 8) Networking (프로젝트: Neutron)
  + 인스턴스의 네트워크를 제공
  + DHCP, VLAN, 플로팅 IP 등 기능을 제공
  + Firewall, Load Balancer, VPN, IDS/IPS NFV 기능 제공
  + 다양한 네트워크 벤더나 기술들에 적용가능한 플러그인 아키텍처를 제공
  
 ### 9) Dashboard (프로젝트: horizon)
  + 오픈스택 환경을 운영 및 관리 할 수 있는 웹 기반의 셀프 서비스 포탈 인터페이스를 제공
  + 오픈스택 API 또는 Amazon Web Server API지원
  
  ***
 
 ## 오픈스택 노드 종류
  ### 컨트롤러 노드
   + keystone
   + Horizon
   + Nova
     + openstack-nova-api
     + openstack-nova-scheduler
   + Glance
   + Cinder
   + Neutron
   + Heat
   + celiometer
   
 ### 컴퓨터 노드 
  + nova
  + Ceilometer
  + neutron
  
 ### 네트워크 노드 : 1대
  + Neutron
  + Ceilometer
  
 ### 스토리지 노드 : 8대 / 14대
  + Swift (8대)
    + Proxy 3대
    + storage 5대 이상
  + Ceph (14대)
   + Mon: 3대
   + OSD: 5대
   + RGW: 2대
   + MDS: 3대
    
 프로젝트 = Component(구성요소) = 서비스
 
###
 #### 컨트롤러 노드
  + 노드들 중에서 가장 중요한 노드이다.
  + 설치되어있는 오픈스택노드들에 상태를 확인 할 수 있다.
  
 #### 컴퓨트 노드
  + 인스턴스(가상머신) 
  + 호스트의 특징을 가지고있다
  + 타입2형태의 하이퍼바이저
 
 #### 네트워크 노드
  + 네트워크 통신을 할때 반드시 네트워크 노드를 거쳐야 함
  + 외부브릿지를 통해서 밖으로 통신가능하고 ip a s br -ex 확인 할 수 있다.
  + ip a s br -ex 는 반드시 네트워크 노드에만 있어야 한다.
 
 #### 스토리지 노드
  + swift보다 좋은 기능이 많아져서 사용을 안함
  + 오픈스택에서 가장 적합한 스토리지는 ceph이다. 그 이유는 많은 기능을 가지고 있기 때문이다.
  + Cinder는 중개자 역할이고 오픈스택 스토리지 역할은 하지않음
  + cinder -> Backend storage (Lvm은 복구시스템이 없어서 안정성이 떨어짐 / ceph와 glusterfs는 복구 시스템이 있음 cinder는 ceph와 gluster를 노드와 연결하는 중개자)
*** 

## 오픈스택 실습

### 1 ) Controller 서버

- Cpu 2코어
- Memory 8192
- **구성 노드**
- Controller
- Network
- Storage

### 2 ) compute 서버

- cpu 2
- Memory 4096
- **구성 노드**
- Compute

1) 오픈스택 노드 상태 확인패키지 설치
```
yum -y install openstack-utils

→ 설치하면 openstack-status

 오픈스택 노드 상태 확인 커맨트 활성화
```
2) 오픈스택 관리웹페이지 접속
```
 openstack-utils 를 설치하면 루트 디렉토리에
 answers.txt  keystonerc_admin 에 오픈스택관리자 계정정보가 들어가있다.
 
 
 우리는 프로젝트와 identity를 사용할 것이다.
 회사에서 각각 프로젝트를 할당 할 수 있다.

```

### 오픈스택 이미지 다운로드 경로
 + https://docs.openstack.org/image-guide/obtain-images.html
 + 위 경로에서 Centos 7 버전으로 다운을 받았다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_image_download.png" alt="drawing" width="350"/>
  
