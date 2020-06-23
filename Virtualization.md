# 가상화 기본적인 개념학습 및 실습과정
  ### 가상화를 사용하는 이유는?
   
   + **가상 시스템은 서로 독립적**
     + **가상화의 최종목적 (Isolation)으로 하나의 서버나 시스템에 문제가 생겼을때 다른 서버와 시스템에 영향이 가지않도록 분리(격리)한다.**
     
   + 한대의 시스템을 다수의 가상 시스템으로 분할해서 사용
   
   + 리소스를 효율적으로 사용
   
   + 서버를 빠르고 쉽게 배포
   
   + 중앙집중화된 가상화 인프라 구성 가능
   
***
#### 기본적으로 실습한 환경은 Centos 7.8 버전
#### 1. ovirt (Hypervisor Managerment)
  ##### (1) 기본 네트워크
  ```
  IP = 192.168.122.10
  Hostname ovirt.abc.local
  ```
  ##### (2) ovirt 설치하기
  + **Redhat 계열이기때문에 Debian 계열인 Ubuntu에서는 설치 할 수 없음!**
  ```
   yum update // 로 설치되어있는 패키지 최신버전업데이트
   yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release43.rpm
   커널업데이트 후에 reboot로 최신커널버전으로 실행되는지 확인
   yum install ovirt-engine
  ```
  
  ##### (3) engine-setup 명령어로 Manager구성
  ```
  **engine-setup (대화식설치) <- 파일생성하지않고 기본값으로 설치진행함**
  engine-setup --generate-answers=FILE
  engine-setup --config-append=FILE
  ```
  ##### (4) 설치완료
  ```
  유저아이디 ' admin@internal '
  /etc/hosts 에 ip와 로컬주소 입력
  web에 ip주소로 들어가서 로그인해주면 관리자페이지로 접속완료
  ```
  + **관리자 주소는 절대로 밖으로 노출되어서는 안된다.**





#### 2. KVM 1 (Hypervisor)
```
trick

IP = 192.168.122.21
hostname = hyper1.abc.local
yum update
reboot 커널업데이트
yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release43.rpm
yum install qemu-kvm libvirt virt-install bridge-utils vdsm vdsm-client
```

#### 3. KVM 2 (Hypervisor)
```
thin

IP = 192.168.122.22
hostname = hyper2.abc.local
yum update
reboot
연결

ovirt서버에서 호스트 추가하는 과정에서 오류가 발생한다면
호스트가 되는 VM에 cpu를 지금 사용하는 컴퓨터와 cpu를 같은것을 사용하도록 복사해준다.

```


***

### 가상화 용어 기본개념
  + 커널(kernel) https://en.wikipedia.org/wiki/Kernel_(operating_system)
  + 보호링(protect ring) https://en.wikipedia.org/wiki/Protection_ring
  + *하이퍼바이저(hyperviser)* https://en.wikipedia.org/wiki/Hypervisor
  + 가상랜(VLAN) https://en.wikipedia.org/wiki/Virtual_LAN
  + 가상화의 핵심은 분리 / 격리 (isolation)
  + 하나의 운영체제안에서는 프로세스간의 통신을 하기위해서는 IPC(inter process communication) https://en.wikipedia.org/wiki/Inter-process_communication 가 필요하다.
  + QEMU(Quarterdeck expanded memory manager) https://en.wikipedia.org/wiki/QEMU * full virtualization
  + KVM (Kernel-based Virtual Machine) https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine * para virtualization
  + TCP/IP 가이드 http://www.tcpipguide.com/

***
## 가상화 종류
 ### Full virtualization (전체)
  ###### VMware가 대표주자
  + **장점**
    + 가상머신이 제공받은 하드웨워 모두가 가상 하드웨어
    + 제공받은 가상머신 하드웨어들은 자신이 가상인지 알지 못함
    + 물리적인 하드웨어에 접근할때 하이퍼바이저에 의해 제어
    + 대부분의 운영체제를 쉽게 설치가능
  + **단점**
    + 전 가상화는 트랩(변환)과 에뮬레이터 작업을 거치기때문에 성능이 저하 (오버헤드가 많음)
    + 또한 Sensitive instruction이 발생하면 하이퍼바이저에 문제가 발생
     + 하드웨어 지원으로 해당문제 해결가능
 
 ### Para virtualization (반)
  ###### Xen -> KVM 으로 이동 지금은 전가상화로 지원
  + 운영체제의 커널 소스를 수정한 가상화
  + 하이퍼바이저가 가상머신에게 특수한 인터페이스 제공
   + 벤더마다 반가상화의 인터페이스가 다름
   + KVM에서는 hypervisor-aware 드라이브라고 함
  + **반가상화는 전가상화보다 오버헤드가 적음**
  + 운영체제의 커널 소스를 수정해야하기 때문에 오픈소스 운영체제 한정
  
  ***
  
### 하이퍼바이저란?
  + 하드웨어를 소프트웨어적으로 파티셔닝하며 가상머신에게 제공
  + 주요기능은 시스템 자원관리, 모니터링, 독립성 유지, 주변장치 제공
  + **가상화에서는 독립성유지가 매우중요**
   + 서로 다른 가상머신에서 실행한 프로세스들은 하나의 물리적인 메모리에서 
 #### 하이퍼바이저 종류
  ##### native or bare-metal virtualization
   + Application -> **Kernel -> Hypervisor** -> Hardware
   + 물리적인 머신에 하이퍼바이저 소프트웨어를 설치
   + 별도의 운영체제가 필요 없음
   + **하이퍼바이저를 관리할 시스템이 필요**
  
  ##### host virtualization
   + Application -> **Hypervisor -> Kernel** -> Hardware
   + 운영체제가 설치된 머신에서 하이퍼바이저 소프트웨어를 설치
   + **하이퍼바이저를 관리할 시스템이 필요하지않음**
   
***

 ### 클라우드 컴퓨팅
 + 가상화는 클라우드 컴퓨팅의 기본 토대
 + 가상화와 클라우드 컴퓨팅은 서로 별개
 + 환경 및 요구사항은 적합한 방식 구성
 + 주요 결정 요인은 예상 작업량
 + 가상화는 특정 응용프로그램에 사용할 리소스가 한정적일 경우에 적합

***
### ovirt 란?
 + Host와 Guset시스템을 중앙에서 관리하는 가상화 플랫폼
 + ovirt에서 제공하는 기능
  + hardware node관리
  + 스토리지 및 네트워크 자원 관리
  + 가상머신 배포 및 관리기능
  + 마이그레이션 및 고가용성
  + 시스템 스케줄링 및 파워관리
  + 각 노드 및 전체적인 플랫폼 모니터링 기능
  
 #### ovirt 구성요소
  + **Engine이란**
   + 물리적 자원과 가상의 자원을 중앙에서 관리하기 위한 플랫폼
   + ovirt의 코어 구성 요소
   + 웹 서비스로 실행되는 JBoss 기반 Java 응용 프로그램 (Wildfly)
   + 데이터는 데이터베이스에 저장 (PostgreSQL)
   + Enterprise Linux 위에 설치
   
 #### **ovirt의 두가지 엔진**
  + **Standalone Manager**
    + 별도의 물리적 시스템 또는 가상화 환경에서 호스트되는 가상 시스템에서 실행
    + 물리적인 시스템으로 주로 배포
    + 배포와 관리가 상대적으로 쉽다.
    + 추가적인 제품을 통해서 외부관리 가능
    
  + **Self-Hostd Engine**
    + 엔진이 관리하는 ovirt 환경에 가상시스템으로 설치
    + 실제서버가 하나가 더 적음
    + 고가용성
    + POC 용도로 사용하거나 작은환경에서 적합
    
 #### **KSM 기법**
   + KVM의 메모리관리 기법
   + Host 시스템에서 Guest OS가 동일하면 메모리의 페이지를 공유
   + 메모리 페이지 공유 -> 메모리 오버커밋
   + 오버헤드 또는 페이지 폴트 발생원인
 #### 장치모델
  + Guest가 실제로 Hardware에 접근하는 것은 불가능
  + 실제 Hardware와 같은 역할을 할 가상의 Hardware가 필요
  + Guest에 에뮬레이트된 가상의 Hardware를 제공
  + Qemu를 통한 Hardware 에뮬레이트
  
 #### Virtlo
  + 에뮬레이터된 가상의 Hardware는 실제 Hardware보다 성능이 안좋음
  + 반가상화 I/O 장치를 Guest에게 부여
  + 이를 위해서 Guest 시스템에서 추가 드라이버를 설치해야 함
  + 벤더마다 이 반가상화된 장치에 대한 인터페이스가 다름
  
***
+ Java Web Application

+ Web Server (Apache, nginx)

+ Web Application (WAS)
  + opensource = Jboss -> Wildfly
  + Enterprise = JBoss ES

+ SAN (Storage Area Network)

+ FC-SAN : Fiber Channel
  + HBA (Host Bus Adapter) : FC
  + FC Protocol
  + SAN Switch
  
+ IP-SAN (iSCSI, FCoE(FC over Ethernet) ...)
  + Ethernet NIC
  + TCP/IP Protocol
  + Ethernet Switch
  
+ VoIP (Voice over IP)
+ VoLTE (Voice over LTE)

***

#### 가상화 프로그램 종류
  ##### Type 1 (Bare-metal / Native)
  ###### Hypervisor

  + VMware ESXi(ESX) = 운영체제에 프로그램을 더하는방식으로 설치가능
  + Citrix Xen Server (Xen opensource) = 리눅스에서만 가능 
  + Redhat RHEV(KVM) = 리눅스에서만 가능
  + Microsoft Hyper-V = 윈도우는 기능을 추가해줘야 사용가능 (윈도우는 운영체제 밑으로 Hypervisor가 설치/제거가되기에 재부팅해줘야함)

  ###### Virtualization Managerment
  + VMware VCenter
  + Citrix VCenter
  + ReHat RHV
  + Microsoft System Center Virtual Machine Manager(SCVMM)


  ###### VMware vSphere = ESXi + VCenter
  ###### Citrix Xen = Xen Server + Xen Center
  ###### *Redhat RHV = KVM + oVirt (내가 이용한 패키지)
  ###### Microsoft = Hyper-V + SCVMM


##### Type 2 (Hosted)
  ###### 일반적으로 개발용으로 사용
  + VMware Workstation/Fusion (유료)
  + Oracale VirtualBox (무료이면서 모든 운영체제에서 이용가능) //내부적으로 KVM소스로 만들어짐


***

#### 가상화머신에 의한 대락적인 성능차이
  + 기본 bare-metal system을 기준으로 1이라고 한다면
  + bare-metal virtualizion은 0.8
  + host virtualizion 0.6
  app과 하드웨어간에 거치는 경로가 많아진다면 속도가 느려짐
  
***

