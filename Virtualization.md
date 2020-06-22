## 가상화 기본적인 개념학습 및 실습과정
#### 1. ovirt (Hypervisor Managerment)
  ##### (1) 기본 네트워크
  + IP = 192.168.122.10
  + Hostname ovirt.abc.local
  ##### (2) ovirt 설치하기
  + yum update 로 설치되어있는 패키지 최신버전업데이트
  + yum install http://resources.ovrit.org/pub/yum-repo/ovirt-release43.rpm
  + 커널업데이트 후에 reboot로 최신커널버전으로 실행되는지 확인
  + yum install ovirt-engine

  ##### (3) engine-setup 명령어로 Manager구성
  + engine-setup (대화식설치) <- 파일생성하지않고 기본값으로 설치진행함
  + engine-setup --generate-answers=FILE
  + engine-setup --config-append=FILE





#### 2. KVM 1 (Hypervisor)
+ IP = 192.168.122.21

#### 3. KVM 2 (Hypervisor)
+ IP = 192.168.122.22

***

### ovirt 구성요소

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
  
+ PSTN (전화망 Circuitket-Switching)
+ VoIP (Voice over IP)
+ VoLTE (Voice over LTE)

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

### native or bare-metal virtualization
  <img src="https://drive.google.com/drive/my-drive"></img>

### host virtualization

### Full virtualization (전체)
  ###### VMware가 대표주자
  + 
### Para virtualization (반)
  ###### Xen -> KVM 으로 이동
  +

***

#### 가상화머신에 의한 대락적인 성능차이
  + 기본 bare-metal system을 기준으로 1이라고 한다면
  + bare-metal virtualizion은 0.8
  + host virtualizion 0.6
  app과 하드웨어간에 거치는 경로가 많아진다면 속도가 느려짐

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
