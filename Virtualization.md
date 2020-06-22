### 가상화의 핵심키워드
+ 커널(kernel) https://en.wikipedia.org/wiki/Kernel_(operating_system)
+ 보호링(protect ring) https://en.wikipedia.org/wiki/Protection_ring
+ 하이퍼바이저(hyperviser) https://en.wikipedia.org/wiki/Hypervisor
+ 가상랜(VLAN) https://en.wikipedia.org/wiki/Virtual_LAN
+ 가상화의 핵심은 isolation
+ 하나의 운영체제안에서는 프로세스간의 통신을 하기위해서는 IPC(inter process communication) https://en.wikipedia.org/wiki/Inter-process_communication 가 필요하다.


### native or bare-metal virtualizion
[Google](

### host virtualizion

### Full virtualizion(전체)
###### VMware가 대표주자
+ 
### Para virtualizion(반)
###### Zen -> KVM 으로 이동

#### 가상화머신에 의한 대락적인 성능차이
+ 기본 bare-metal system을 기준으로 1이라고 한다면
+ bare-metal virtualizion은 0.8
+ host virtualizion 0.6
app과 하드웨어간에 거치는 경로가 많아진다면 속도가 느려짐

#### 가상화 프로그램 역사와 종류
##### Type 1 (Bare-metal / Native)
###### Hypervisor

+ VMware ESXi(ESX) = 운영체제에 프로그램을 더하는방식으로 설치가능
+ Citrix Xen Server (Xen opensource) = 리눅스에서만 가능 
+ Redhat RHEV(KVM) = 리눅스에서만 가능
+ Microsoft Hyper-V = 윈도우는 기능을 추가해줘야 사용가능 (윈도우는 운영체제 밑으로 Hypervisor가 설치/제거가되기에 재부팅해줘야함)

###### Virtualizion Managerment
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
