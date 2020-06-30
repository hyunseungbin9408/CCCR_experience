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
  + 인스턴스(가상머신, 서버)의 생성, 중지, 스케쥴링 등 인스턴스의 라이프사이클을 관리
  + KVM, Xen, VMware 등 하이퍼바이저 기술 사용
  + 오픈스택에서 CPU, Memory 등을 제공
  
 ### 2) Identity (프로젝트: Keystone)
  + 모든 컴포넌트의 인증을 담당
  + LDAP과 같은 기술을 사용하여 사용자의 중앙 디렉토리 기능을 함
  + 각 서비스의 주소와 토큰을 관리
  
 ### 3) Image (프로젝트: Glance)
  + 인스턴스를 생성하기 위한 운영체제 디스크 이미지를 제공 (Qcow2, Ova)
 
 ### 4) Object Storage (프로젝트: Swift)
  + 사용자가 사용 할 수 있는 클라우드 스토리지
  + Http 기반의 RESTful API를 제공
  + 수평 확장 가능한 분산 스토리지
  + 복사본을 구성하여 안전한 대용량 스토리지
  
 ### 5) Orchestration (프로젝트: Heat)
  + 탬플릿 기반으로 다양한 클라우드 어플리케이션을 배치 및 관리 할 수 있는 오케스트레이션 기능제공
 
 ### 6) Telemetry (프로젝트: Ceilometer)
  + 오픈스택 전체 환경을 에이전트 기반으로 데이터 수집
  + 수집한 데이터로 모니터링, 사용량, 벤치마킹, 확장성, 통계 등을 제공하는 서비스
  
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
