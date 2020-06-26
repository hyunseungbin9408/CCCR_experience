# 데이터 센서 및 클러스터 생성
 ## 데이터 센터란?
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Datacenter_model.png" alt="drawing" width="450"/>
 
 + 모든 물리적 및 논리적 자원을 포함한 최상위 조직 객체
 + 단일 데이터 센터는 독립적인 가상화 환경
 + 데이터센터에서는 데이터안정성이 중요하기때문에 호스트에서 나오는 모든 데이터를 저장 하고 관리 할 수 있는 독립적인 스토리지 서버가 필요하다.
 + 스토리지 서버에도 또한 백업서버를 만들어 만에하나 생길 수 있는 변수도 대비해야 한다.
 
 ## ovirt관리모드에서 데이터 센터생성
  ### 데이터센터 생성
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/new_datacenter.png" alt="drawing" width="450"/>
  
   + 스토리지유형은 기본값으로 공유됨으로 설정되어있고 그대로 진행하였다.
   + 쿼터모드는 기본적으로 비활성화되어있다.
   ```
    쿼터모드란?
    쿼터는 Red Hat Virtualization에서 제공되는 리소스 제한 도구다.
    쿼터를 통해 메모리, CPU, 스토리지에 대한 사용자 액세스를 제한할 수 있다.
   ```
   +
 
  ### 클러스터 생성
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/new_cluster.png" alt="drawing" width="450"/>
  
   + **클러스터를 생성할때 관리 네트워크 필수**
   + 스위치유형은 Linux Bridge 와 OVS (open v switch : 가상의 스위치를 만들어줌)
   
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/new_cluster2.png" alt="drawing" width="450"/>
  
   + 좌측 메뉴 최적화에 메모리최적화를 서버용 로드로 바꿔줌
   + 메모리 Ballon 최적화 사용
   ```
    메모리 Ballon이란 같은 호스트(제한된 메모리크기)에 여러 대의 가상머신이 있을때 메모리가 더욱 필요한 곳으로 최적화 시켜주는 방법
   ```
   + KSM 활성화 사용
   ```
    KVM의 메모리관리 기법
    Host 시스템에서 Guest OS가 동일하면 메모리의 페이지를 공유
    메모리 페이지 공유 -> 메모리 오버커밋
    오버헤드 또는 페이지 폴트 발생원인
  ```
  ### 스토리지 컨테이너
   + 스토리지 도메인에 대한 연결 정보
   + 스토리지 유형 및 스토리지 도메인 정보가 저장
   + 해당하는 데이터 센터의 모든 클러스터에서 사용 가능
   + 모든 호스트 클러스터는 같은 스토리지 도메인에 액세스 가능
   
  ### 네트워크 컨테이너
   + 데이터 센터의 논리 네트워크 정보가 저장
   + 네트워크 주소, VLAN 태크 및 STP 지원 등의 상세 정보도 포함
   + 트래픽 분리를 위해 다수의 논리 네트워크 구성 가능
   
***

 ## 클러스터란?
  + 여러 대의 시스템을 하나의 시스템처럼 논리적으로 묶어서 사용하는 것
  + **클러스터의 핵심은 마이그레이션**
   
  
  ##### Cluster의 종류는 두가지
 + HPC (High Performence Computer)
 + 고성능 컴퓨터라는 뜻이고 비용이 많이 들기때문에 일반적으로 사용하기 버겁다.
 
 + **HA (High ability)**
 + 시스템의 가용성을 높이기 위한 방법중 하나이다. 하나의 호스트에 장애가 생겼을 때 연결된 다른 호스트의 컴퓨터가 서비스를 이어받아계속해서 서비스되도록 한다.
 + 모든 호스트에 데이터가 스토리지 서버로 들어가면서 호스트서버에 문제가 생기더라도 데이터를 보존 할 수 있다.
 + 스토리지 서버도 백업 할 수 있는 서버를 만들어서 데이터 백업이 반드시 될 수 있도록 해야 한다.
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Cluset_model.png" alt="drawing" width="450"/>
  
 ### 데이터센터에서 클러스터
  + 동일한 아키텍처 및 cpu 모델을 공유
   + 혼합 사용시 공통기능만큼만 다운그레이드
  + 특정 데이터 센터에 속하는 호스트그룹
  + 가상 시스템의 마이그레이션 도메인
  
***
  
 ## 가상머신 생성
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/VM_create.png" alt="drawing" width="450"/>
 
  + 템플릿이란 복제해서 사용할 수 있도록 도와주는 시스템 
  
  + 운영시스템은 자동화에 도움을 줄 수 있도록 운영체제에 맞게 반가상화 드라이버, 맥주소나 네트워크 주소들을 자동으로 부여해주기 때문에 운영시스템은 정확하게 부여 해주는것이 중요
  
  + 인스턴스 유형은 여기에서는 VM이라고 한다. 유형은 선택하면 VM에 크기를 고를 수 있다. (일반적으로 사용자 정의를 사용함)
  
  + 최적화 옵선은 데스크탑, 서버, 고성능을 고를 수 있다. (우리는 서버를 선택)
  
  + **이름과 설명 코멘트를 쓸 수 있는 칸들이 있는데 설명과 코멘트는 정확하게 전달할 수 있도록 구체적으로 적는것이 중요**
  
  + 인스턴스 이미지는 가상 디스크를 뜻하고 우리가 만드는 가상머신에 사용할 디스크를 뜻한다. 지금은 디스크이미지파일을 만들지 않았기 때문에 생성한다. 
  
  ```
  지금 가상머신은 생성되었지만 부트파일이 없어서 ovirt서버에 centos7minimal 버전을
  
  wget 으로 다운받고 
  
  engine-iso-uploader -i nfs-iso upload FILE 로 ovirt서버 nfs-iso 에 업로드를 해준다.
   
  ovirt관리메뉴에서 가상머신 -> 부팅옵션을 넣기위해서 전원이 꺼져있는 가상머신 실행메뉴옆에 한번실행으로 부팅옵션에서 올려둔 iso파일을 추가해주고 설치를 시작한다.
  
 // 한번실행으로 설치하는 이유는 부트옵션에서 cdrom을 장착하면 이후에 가상머신에서 부트장애가 발생하였을때 하드디스크에서 cdrom으로 넘어가기때문에 귀찮은 일이 발생 할 수 있으니 가상머신에 iso파일로 설치할때에는 한번만 실행으로 설치를 해야 한다.

```
 ## 마이그레이션 특징
  + **마이그레이션에 핵심은 CPU**
  + 마이그레이션을 하기위해서는 cpu 모델 특징이 같아야한다.
  + 각 하이퍼바이저위에 가상머신을 다른 하이퍼바이저로 마이그레이션을 할때 서로 다른 cpu를 사용한다면 더 좋은 cpu를 하향평준화 시켜서 마이그레이션을 한다. (1cpu 0.8cpu가 있으면 0.8로 기능을 통일시킴)


 ## 네트워크 설정
  + 네트워크 전송단위는 패킷이 아니라 프레임이다.
  + 프레임 구성 헤더 와 H3주소 H4주소가 들어가는 바이트를 제외한 공간만 사용가능
  + 프레임이 기본적으로 실질적으로 1400바이트이고 최대 9000바이트(앞으로 더욱 커질예정)로 들릴수있다. (MTU)
  + 9000바이트 단위에 프레임을 점보프레임이라고 한다.
  
 ## 디스크
  + Pre-Allocation (Thick)
  
  + Thin Provisioning을 지원하는 파일형식
    + qemu/kvm: qcow2
    + virtualbox: vdi
    + hyper-v: vhd, vhdx
    + vmware: vmdk
    
  + raw파일 qemu-img convert -O vmdk a.raw a.vmdk 처럼 변환가능
  
  ## 템플릿 관리
  
  ### 템플릿을 왜 사용하는가?
   + 미리구성된 가상 시스템의 복사본
   + 유사한 가상 시스템 배포에 유리
   + Clonezilla 또는 Ghost등과 유사
   + 템플릿 기반 컴퓨터 사용시 메모리 사용량 감소
   + 이미지 씰링 작업이 필요 (MAC주소, 인증서 등의 고유정보 제거)
    + virt-sysprep 을 이용한 이미지 씰링가능
    
  ### 템플릿 생성
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/new_vm_template.png" alt="drawing" width="450"/>
  
   + 새 템플릿을 생성하기 위한 모델인 가상머신을 설치한다.
   + 기본 정보들을 다 삭제 이미지 실링을 한다
   + 이번에 실습한 환경에서는 virt-sysprep을 사용하지않았다.
   + **템플릿을 생성할 때 꼭 봉인체크를 해주어야한다(실링)**
   + **템플릿에는 고정아이피가 정해지면 안되고 DHCP를 이용해서 자동할당해야한다.**
   
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/new_vm_template_setting.png" alt="drawing" width="450"/>
  
   + 템플릿에는 기본 사용자설정이 중요하다
   + 템플릿으로 가상머신을 만들때 호스트네임을 설정 할 수 있다.
   + **템플릿에 기본적으로 암호가 설정되어있다면 누구나 서버설정을 변경 할 수 있기 때문에 암호를 설정 하면 안된다.**
   
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/new_vm_template_setting_userscript.png" alt="drawing" width="450"/>
  
   + 템플릿에서 가장 중요한 사용자 지정 스크립트를 지정 할 수 있다.
   + 스크립트명령어
   ```
   // 스크립트명령어로 아파치서버 설치 및 작동예시 
     #cloud-config
     runcmd
     - [ yum, update, -y]
     - [ yum, install, httpd, -y]
     - [ systemctl, start, httpd]
     - [ systemctl, enable, httpd]
     - [ firewall-offline-cmd, --add-service=추가할서비스] // 오프라인상태에서 방화벽을 설정할때에는 offline명령어를 추가해줘야한다.
     오프라인 명령어 없이 명령어를 입력한다면 selinux가 사전에 차단하기 때문에 명령어가 적용이 되지않는다.
     참고로 스크립트 명령어는 --permanent를 사용 할 수 없다.
     스크립트 명령어에는 명령어가 끝날때마다 콤마(,)를 찍어줘야한다.
   ```    
   ### Cloud-config 스크립트 명령어
   + 예시와 활용방법 https://cloudinit.readthedocs.io/en/latest/topics/examples.html
 ### 템플릿으로 만든 가상머신에 ssh로 접속하기
  
