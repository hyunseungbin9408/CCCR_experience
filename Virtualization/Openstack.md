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
  
  + 각 서비스의 주소(API)와 토큰을 관리
  
 ### 3) Image (프로젝트: Glance)
  + 인스턴스를 생성하기 위한 운영체제 디스크 이미지를 제공 (Qcow2, Ova)
  
  + 디스크나 서버 이미지에 대한 API 요청과 최종 사용자와 OpenStack Compute 구성 요소로부터의 메타데이터 정의를 허용
  
  + OpenStack 오브젝트 스토리지를 포함한 다양한 스토리지 타입에서 디스크나 서버 이미지 저장을 지원
 
 ### 4) Object Storage (프로젝트: Swift)
  + 레드햇 오브젝트스토리지 설명 : https://www.redhat.com/ko/topics/data-storage/file-block-object-storage
  + 사용자가 사용 할 수 있는 클라우드 스토리지
  
  + Http 기반의 RESTful API를 제공
  
  + 수평 확장 가능한 분산 스토리지
  
  + 복사본을 구성하여 안전한 대용량 스토리지
  
  + swift 서비스
    + swift-proxy
    + swift-account
    + swift-container
    + swift-object
    
  + swift 구조

  + ceph 스토리지 소개
  
  + 파일시스템 스토리지 (NFS/SMB/Glusterfs)
    + inode (권한,소유권,파일의 위치=섹터정보)
    + 계층적 구조
    + 파일을 어떻게 찾아갈지 정해주는 시스템
    + 사용하기가 편해진다.
    + 단점
    + 파일이 많으면 느려진다(오래되면 느려진다).
    + 사이즈의 제약이있다.
    + load average -> 0.8 이상이면 위험
    + storage usage => 80%
    + fat32(5G) => NTFS
    + ext4(ubuntu) / xfs = EXABYTE급으로 용량 제한(500TB)이 없음 (centos)
  + 블록 스토리지(isCSI)
    + 가장 성능이 좋은 스토리지
    + 직접 접근해서 사용 할 수 없음
    + 파일 시스템포맷 필요
    
  + 오브젝트 스토리지(Swift/Ceph)
    + 고유값 사용 (해시값 = 확인하는 명령어 md5sum )
    
    <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/hash%20function_comman_hashfunction.png" alt="drawing" width="500"/>
    
    + 수평적 구조
    + 발렛파킹같은 구조
    + 오브젝트로 형태로 저장 (이진데이터+메타데이터)
 ### 5) Orchestration (프로젝트: Heat)
  + 탬플릿 기반으로 다양한 클라우드 어플리케이션을 배치 및 관리 할 수 있는 오케스트레이션 기능제공
  
  + OpenStack 서비스들과 관련한 측정 데이터를 효율적으로 수집
  
  + 스택을 만들고 템플릿으로 간편하게 장치들을 구성 할 수 있음
 
 ### 6) Telemetry (프로젝트: Ceilometer)
  + 오픈스택 전체 환경을 에이전트 기반으로 데이터 수집
  
  + 수집한 데이터로 모니터링, 사용량, 벤치마킹, 확장성, 통계 등을 제공하는 서비스
  
  + 서비스들로부터 발송된 notification을 모니터링하여 이벤트와 측정 데이터를 수집
  
  + 데이터 저장소와 메시지 큐를 포함한 다양한 목적지에 수집한 데이터를 발행
  
 ### 7) Block storage (프로젝트: Cinder)
  + 인스턴스의 영구 저장장치인 블록장치를 제공
  
  + 블록 스토리지 장치를 생성, 관리 할 수 있도록 플러그인 가능한 드라이버 아키텍처 구조
  
  + 다수의 스토리지를 멀티백엔드로 사용 가능 (LVM, NFS, Glusterfs, Ceph)
  
  + (LVM, NFS, Glusterfs, Ceph) 장치만에 장점을 이용해서 각각 백엔드 스토리지에 추가 할 수 있음
  
  + 볼륨을 생성하면 compute에 생성되어짐
  
  + flavor는 인스터스에 종속되고 인스턴스가 삭제될때 같이 데이터가 삭제되기 때문에 volume에 백업 할 수 있음
  
  + 볼륨 스냅샷 : 특성 시간대에 디스크 상태를 저장하는 단계
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_backup_snapshot_storage.png" alt="drawing" width="600"/>
  
  + backup은 object storage에 저장

  + 스냅샷은 같은 스토리지에 저장되는것이라 백업이랑은 다른 형식
  
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
  
  ***
 
 ### 네트워크 노드
  + 네트워크 통신을 할때 반드시 네트워크 노드를 거쳐야 함
  
  + 외부브릿지를 통해서 밖으로 통신가능하고 ip a s br -ex 확인 할 수 있다.
  
  + ip a s br -ex 는 반드시 네트워크 노드에만 있어야 한다.
  
 #### 프로바이더 네트워크 = 외부 네트워크 = 외부망
  + 가상 네트워크와 물리 네트워클 연결
  + 관리자 역할을 사용해야함
  + flat
  + vlan
  + vxlan
  + gre (터널링)
  
 #### 프로젝트 네트워크 = self-tenancy network = 테넌트 네트워크 = 내부 네트워크 = 프라이빗 네트워크
  + 프로젝트 내에서 인스턴스가 사용하는 가상의 네트워크
  + 일반 사용자 역할을 사용하여 생성 가능
  + vlan
  + vxlan
  + gre (터널링)
 
 #### neutron 플러그인
  + ML2 사용하여 다수의 네트워킹 기술을 사용 가능
  + Linux Bridge
  + OVS (Open vSwitch) -> OVN (Open Virtual Network)
  + SRIOV
  + MacVTap
  + L2 population
  + OpenDaylight / OpenContrail (OpenSource)
  
 #### OVS 브릿지
  + br-int
  + br-ex 
    + 외부와 통신 할 때 반드시 거쳐야하는 브릿지
  + br-tun
  
 #### SNAT (Source Network Address Translation)
  + 통신할수 있도록 시작 네트워크를 바꿔주는 것
  + 라우터에 도착했을때 변환시키는 과정 (source : 192.168.3.14 destination: 0.0.0.0/0 to: 10.0.0.115)
  
 
 #### DNAT (Destination Network Address Translation)
 
  
 ***
 #### 스토리지 노드
  + swift보다 좋은 기능이 많아져서 사용을 안함
  
  + 오픈스택에서 가장 적합한 스토리지는 ceph이다. 그 이유는 많은 기능을 가지고 있기 때문이다.
  
  + Cinder는 중개자 역할이고 오픈스택 스토리지 역할은 하지않음
  
  + cinder -> Backend storage (Lvm은 복구시스템이 없어서 안정성이 떨어짐 / ceph와 glusterfs는 복구 시스템이 있음 cinder는 ceph와 gluster를 노드와 연결하는 중개자)
  
  + 영구적인 스토리지 (Persistent Storage)
    + Cinder => Block Storage
    + Swift => Object Storage
  
  + 일시적인 스토리지 (Ephemeral Storage)
    + /var/lib/nova/instances/VMID/disk => Block Storage
*** 

###
### Orchestation
 + Heat => Orchestration
 + Stack => 템플릿파일이 필요함 (image)

 #### openstack resource
  + Yaml 
    + key : value (value => root:toor)
    
  + list 형태
    + key:
     + - value1
     + - value2
     + - value3
  
  + 
  
 #### 검색 : Openstack heat template guide
  + Openstack사이트: https://docs.openstack.org/heat/pike/template_guide/hot_guide.html#template-input-parameters
  + 가이드에서 확인 할때 앞에 list 형태면 공백 두칸
 #### HOT 파일 구조
  + description : 파일에 대한 설명 
  + heat_template_version: 2016-04-08
  + parameters : 변수를 저장하는 공간
  + resources : 스택에 생성할 자원들 // 제일 중요함
    + vm(내가마음대로정하는 이름):
    +  type: OS::NOVA::SERVER
    +  properties: 
    +   flavor: {get_param: flavor(변수)} // falvor1 처럼 정적으로 넣을 수도있다/
    +   image: {get_param: image(변수)}
    +   keyname
    +   networks:
    +     - network: {get_param: network} // 네트워크 한개면 이렇게
    +       fixed_up: VALUE
    +     - netwrok: {get_param: network2} // 두개를 넣으려면 이렇게 두개
    +   security_groups: [default, web] 
    +
    + 
  + outputs : 스택에서 필요한 정보들을 찾을 수있게 출력하는 서비스
  
### 오픈스택 이미지 다운로드 경로
 + https://docs.openstack.org/image-guide/obtain-images.html
 
 + 위 경로에서 Centos 7 버전으로 다운을 받았다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_image_download.png" alt="drawing" width="350"/>
  
 **오픈스택에서의 스냅샷은 템플릿에 의미처럼 새로운 인스턴스를 만들때 쓰인다.**
