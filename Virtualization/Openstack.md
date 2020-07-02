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

### Controller 서버 (admin관리자)

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
3) 오픈스택 관리자 웹페이지 사용자 관리

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_usercreate.png" alt="drawing" width="400"/>

```
 인증탭에서 사용자를 클릭하고 생성 할 수 있다.
 이름과 암호를 입력해주고 원하는 프로젝트에 속하고 역할도 부여해 줄 수 있다. // 어느 한 프로젝트에 admin역할이 된다면 모든 프로젝트를 관리 할 수 있다.
 사용자에게 역할을 하나하나 부여할 필요없이 그룹묶어서 한꺼번에 역할을 부여해 줄 수 있다. 
 ```
4) 오픈스택 관리자 시스템정보확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_systeminfo.png" alt="drawing" width="400"/>

```
 왼쪽상단 관리탭에서 시스템정보를 확인 할 수 있다. Endpoint로 주소를 확인 할 수 있는데 노드마다 주소가 각각 다르다.
```
5) 오픈스택 관리자 flavor 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_flavor_create.png" alt="drawing" width="400"/>

```
flavor를 통해서 우리는 인스턴스 배포시에 RAM, 디스크, CPU 코어 수, 기타 리소스의 크기를 규정해 둘 수 있다.
우리가 생성하고 싶은 centos7 파일에는 기본적으로 8~9GB에 공간이 필요한데 
오픈스택에서 기본적으로 생성되어있는 flavor에는 딱 맞는것이 없어서 생성해야한다.
위에 보는것처럼 조금은 여유있게 만들었다. 타이트하게 만들면 생성시에 거부당 할 수 있기 때문이다.
```

6) 오픈스택 관리자 이미지파일 공유파일로 등록

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_image_create.png" alt="drawing" width="400"/>

```
이미지 파일을 공용으로 등록해서 필요할 때마다 사용 할 수 있도록 생성하려고 한다.
관리자 계정으로 접속하고 이미지파일을 생성해야 공용으로 만들 수 있고 사용자계정으로 들어간다면 private(선택불가)으로 생성된다.
오픈스택 전용 iso파일을 다운받고 업로드 후에 포멧은 QCOW2파일형식으로 설정해준다.
이 iso파일은 기본적으로 최소 디스크8GB가 필요하니 스토리지는 8기가이상만 사용할 수 있도록 제한을 두어야 한다.
```

7) 오픈스택 관리자 네트워크 생성 및 관리

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_public_network.png" alt="drawing" width="400"/>

```
 오픈스택 외부망을 생성하는 방법은 먼저 메뉴탭에 프로젝트 -> 네트워크 -> 네트워크생성 
 프로젝트는 남들에게 보여주지 않기위해서 admin 프로젝트를 선택해준다
 그 다음 네트워크 타입은 우리가 사용할 수 있는 flat으로 설정한다.
 설정하면 물리네트워크가 등장하는데 extnet으로 설정해준다.
 extnet이란것은 그랩으로 확인 할 수 있다.
 밑에 pools할당은 우리가 할당받는 ip주소의 범위를 정 할 수가 있다. " , " 로 범위를 정할 수 있다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_physicialnetwork_check.png" alt="drawing" width="400"/>

***

### 사용자 계정

1) 프로젝트 내부망 네트워크 생성


<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_create2.png" alt="drawing" width="400"/>

```
 내부망을 설치하는 방법은 프로젝트메뉴에서 네트워크 -> 네트워크생성하면 
 네트워크 이름 후에 서브넷으로 넘어가서 서브넷 이름을 정해주고
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_create3.png" alt="drawing" width="400"/>

```

DNS서버를 정해주는 것이 좋다. // 8.8.8.8로 주소를 주었다.
```

2) 프로젝트 라우터 생성

 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_create_topology.png" alt="drawing" width="40
 0">
 
```
 오른쪽 위에 라우트생성에 들어가서 이름을 넣고 라우트 생성후에 인터페이스를 연결해주면 라우트를 통해서 외부망과 내부망을
 연결한 네트워크가 완성되었다.
```

3) 프로젝트 보안그룹 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create2.png" alt="drawing" width="400"/>

```
 프로젝트 메뉴탭에서 보안그룹으로 가면 기본적으로 생성되어있는 default라는 그룹이 있는데 이 그룹은
 모든 사용자에게 적용시킬 수 있다. 그래서 가상머신을 생성할때 기본적으로 들어가야하는 포트와 서비스를 입력해준다.
 인스턴스로 생성된 가상머신은 원격으로 접속해서 컨트롤하기 때문에 ssh가 필수이다. ssh를 뜻하는 22번 포트와
 네트워크가 제대로 적용되었는지 확인 할 수 있는 ICMP(ping)를 열어주면 된다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create3.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create4.png" alt="drawing" width="400"/>


```
 우리는 워드프레스와 로드밸런스를 구성할 것이기때문에 웹을 구성하는 보안그룹을 만들어준다.
 웹을 구성할때 열어주어야하는 필수 포트 HTTP(80)과 HTTPS(443)을 열어주어야한다.
 이름을 구성하고 보안그룹을 생성하고 전에 했던것처럼 포트를 추가해준다.
```

4) 프로젝트 Floating 

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_Floating.png" alt="drawing" width="400"/>

 ```
 외부망으로 통신 할 수 있도록 유동ip를 설정 할 수 있게 Floating 설정해준다.
 ```
 
5) 프로젝트 컴퓨트 키페어 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_keypair_create.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_keypair_create_key.png" alt="drawing" width="400"/>

```
 컴퓨트 메뉴에서 키페어를 들어가 키페어를 생성할때 이름만 넣어주면되고 생성을 완료하면
 다운로드창이 등장하는데 그것은 개인키를 다운받는것이다. 
 우리는 키페어로 인스턴스를 생성 및 원격실행 할 것이기때문에 컨트롤러 노드에 .ssh폴더에 넣어준다.
 개인키이기때문에 권한을 600 사용자에게만 읽고 쓸수있는 권한을 준다.
```

6) 

### 오픈스택 이미지 다운로드 경로
 + https://docs.openstack.org/image-guide/obtain-images.html
 
 + 위 경로에서 Centos 7 버전으로 다운을 받았다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_image_download.png" alt="drawing" width="350"/>
  
 **오픈스택에서의 스냅샷은 템플릿에 의미처럼 새로운 인스턴스를 만들때 쓰인다.**
