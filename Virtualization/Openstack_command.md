# 우분투에서 오픈스택 원격접속

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_on_ubuntu.png" alt="drawing" width="700"/>

```
sudo apt -y install python-pip

sudo apt  install python3-openstackclient

```
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_python3_command.png" alt="drawing" width="700"/>

```
 예전버전에서는 Nova, cinder, neutron, swift처럼 각각 관리해야했지만
 
 지금은 openstack커맨드로 통합되어짐
 
```
 
## command로 설정방법

```

 Opencstack Resource Action [global option] [resource option]
 
 openstack과 관련된것이 global option이다.
 
 로그인, 헬프 ...
 
 === resource ===
 1. project
 2. user
 3. role
 4. flavor
 5. image
 6. network
 7. subnet
 8. router
 9. security group
 10. key pair
 11. floating ip
 12. volume
 13. server
 14. container
 15. object
 
 === ACTION ===
 1. create
 2. delete
 3. list
 4. show
 5. add
 6. remove
 7. set
 
 ```
 ### 오픈스택 커맨드 자동완성
 
 ```
  openstack complete | sudo tee /etc/bash_completion.d/openstack
  
  이런식으로 적용시켜주고 터미널을 재시작하면 적용된다.
  
```

### 오픈스택 헬프 커맨드

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_server_create_help.png" alt="drawing" width="700"/>

```

 이런식으로 자동완성으로 편하게 원하는 항목에 도움을 얻을 수 있다.
 대괄호제외하고는 필수로 적어줘야한다.
 
 ```


### 오픈스택 커맨드 시작

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_envirment_credential_create.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_envirment_credential.png"  alt="drawing" width="700"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_envirment_credential_info.png" alt="drawing" width="700"/>

```
 오픈스택을 커맨드로 작동하기전에 제일먼저 해야하는것이 오픈스택 사용자와 프로젝트의 환경변수를 적용시키는것
 
 그러기 위해선 오픈스택 우측위 사용자탭에서 OpenStack RC File v3을 다운받아준다.
 
 기본값에서 
 echo "Please enter your OpenStack Password for project $OS_PROJECT_NAME as user $OS_USERNAME: "
 
 read -sr OS_PASSWORD_INPUT

 이 두줄을 삭제하고 
 
 export OS_PASSWORD=$OS_PASSWORD_INPUT
 
 오른쪽에 password_input 에 사용자 비밀번호를 입력하면
 
 실행하고 따로 입력없이 접속이 가능하다.
 
```
### Catalog list (identity)
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_catalog_list.png" alt="drawing" width="700"/>

 + endpoint = API주소 (통신하는것)
 + endpoint의 목록 = catalog
 + public = 외부망과 통신하기위해서
 + internal = 서비스와 서비스간에 통신할때 사용함
 + admin = 관리자가 관리하기 위해서 사용함
 + **중요서비스 Identity(Keystone), message queue(AMQP)**
   + 서비스간에 서비스를 요청할때에는 서비스에 API로 요청하고 그 주소는 Identity가 관리
   + 그 요청을 전달하는 서비스가 AMQP/RabbitMQ이다.
   
***

## 커맨드로 오픈스택 구성하기

 ### 프로젝트 만들기
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_command_project.png" alt="drawing" width="700"/>
 
 ```
 openstack project create project3
 
 으로 커맨드로 입력하면 프로젝트를 만들 수 있다.
 
 ```
 
 ### 유저 만들기
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_command_useradd.png" alt="drawing" width="700"/>
 
 ```
 
 openstack user create --project project1 --password 'dkagh1.' user2
  
 유저를 만드는 커맨드이고 암호에 메타문자가 들어가면 작은따옴표로 묶어준다.
 
 커맨드로 입력 할 때에는 우선분위부터 입력하면 이해하기가 편한 것 같다.
 
 ```

 ### 프로젝트에 유저 권한(role)부여하기
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_command_project_add_user.png" alt="drawing" width="700"/>
 
 ```
 
 openstack role add --project project2 --user user3 _member_
 
 이렇게 입력하면 project2 에 user3가 member라는 권한을 받는데 정확히 확인해보아야한다.
 
 openstack role assignment list --project project2 --user user3
 
 으로 해당 프로젝트에 해당유저의 권한을 알아 볼 수 있다.
 
 openstack role list로 user3은 project2에서 _member_에 권한인것을 알 수 있다.
 
 ```

### Floating IP를 확인하고 인스턴스에 설정하기

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_Floatingip.png" alt="drawing" width="700"/>

``` 
 openstack floating ip list -c 'Floating IP Address' -f value | head -1
 
 위에 커맨드로 지금 프로젝트에 Floating ip 리스트를 확인하는데 'Floating IP Address'를 같이 묶어주지않으면
 
 인식을 못하기 때문에 작은따옴표로 묶어줘야하고 head는 여러가지의 ip중에서 첫번째만 확인하는것인데
 
 이 커맨드 자체를 실행명령어로 만들수 있다.
 
 openstack sever add floating ip instance $(openstack floating ip list -c 'Floating IP Address' -f value | head -1)
 
 위에 명령어를 괄호로 묶어주고 앞에 $을 입력해주면 앞에 server add에 실행명령어로 사용가능해서
 
 인스턴스에 Floating ip를 커맨드로 추가 가능하다.
 
 ```

### image파일 등록 및 삭제

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_image_create.png" alt="drawing" width="700"/>

```

 openstack image create --disk-format qcow2 --file ~/Downloads/CentOS-7-x86_64-GenericCloud.qcow2 centos
 
 먼저 디스크파일형식을 입력해주고 어떤파일을 등록할지 그리고 어떤이름으로 등록할지 정해주면 등록가능!
 
 ```
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_image_delete.png" alt="drawing" width="500"/>
 
 ```
 
 openstack image delete centos
 
 위에 명령어로 프로젝트에 등록된 Image파일을 삭제 할 수 있다.
 
 ```
 
***

 ### Network 설정하기
 
 #### Software Defined Network
   + network Device(control <--> OpenFlow <--> data)
   + ovirt -> Software Defined dataCenter
   + openstack -> Software Defined DataCenter
   
 #### SDN and NFV(Network Function Virtualization)
   + FW <-> Router <-> Switch <-> LB <-> Server
   + VNF1(Virtual Network Function)
   + VNF2(Virtual Network Function)
   + LB -> LBaaSv2
   + LB Service[Project] -> Octaiva
 
 #### Instance 
  + user -> nova-api -> neutron-server -> neutron-dhcp-agent -> dnsmasq
  + instance 가 동적으로 할당이 되어지지않으면 확인해야하는서비스
    + neutron-dhcp-agent.service
    
 #### external network delete
  + 
 
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_Network_help.png" alt="drawing" width="700"/>
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_Network_subnet_help.png" alt="drawing" width="700"/>
  
 ```
 
  새로운 네트워크/서브넷을 만들때 볼 수 있는 도움말들이다.
  
 ```
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_Network_create.png" alt="drawing" width="500"/>
 
 ```
 
 기본적인 외부망 네트워크를 생성할때에는 admin계정으로 전환하고 외부망인지, 
 네트워크 제공 타입과 물리적인시스템방식 을 넣어주고 어떠한 프로젝트에 속하게 할것인지 정하면 완료된다.
 
 ```
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_public_subnet_create.png" alt="drawing" width="700"/>
 
 ```
  
  외부망에 서브넷을 만들어 대역폭과 DHCP를 설정하지않도록 설정하고 프로젝트를 설정하면 서브넷은 설정완료된다.
  
  ```
  
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_Network_sub_create.png" alt="drawing" width="700"/>
 
 ```
  개인 네트워크를 생성하는 명령이고 개인 네트워크는 퍼블릭보다 할것이 없다.
  
  ```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_Network_project2.png" alt="drawing" width="700"/>

```
 
 openstack network list
 
 외부망과 내부망을 한꺼번에 확인 할 수 있는 명령어이다.
 
```

 ### 키페어 만들기
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_keypair_create.png" alt="drawing" width="700"/>
 
 ```
  오픈스택에서 키페어 만드는 커맨드이고 개인 키를 설정해야하는것은 무조건 키값은 나오는데
  
  개인키를 파일로 저장하겠다는 뜻이다.
  
 ```
 
### 보안그룹 설정하기

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_securitygroup_ruleadd.png" alt="drawing" width="700"/>

```
 openstack security group rule create --dst-port 22 default
 
 openstack security group rule create --protocol icmp default
 
 디폴트값에 원격접속 할 수 있도록 22번 포트와 icmp를 넣어준다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_securitygroup_list.png" alt="drawing" width="700"/>

```
 openstack security group rule list default
 
 명령어로 디폴트값에 보안설정이 추가 되었다는 것을 알게되었다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_securitygroupadd_web.png" alt="drawing" width="700"/>

```
 openstack security group create web
 
 명령어로 web이라는 보안그룹을 추가 할 수 있다.
 
 ```
 
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_securitygroup_web_rueladd.png" alt="drawing" width="700"/>

```

 openstack security group rule create --protocol tcp --dst-port 80/443/3306 web

 명령어로 웹에 필요한 http/https/mysql를 다 넣어줄 수 있다.
 
```

***

### 이미지파일 오버디스크 경험

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_server_create_overdisk.png" alt="drawing" width="700"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_server_diskerror.png" alt="drawing" width="700"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Openstack_command_server_create_overdisk_show.png" alt="drawing" width="700"/>

```

이미지파일을 만들려고 설정할때에 기본적인 디스크 여유공간을 미리정해주지않으면 실행은 되어지지만 

부팅과정에서 디스크공간이 부족하다는것을 알게되고 커맨드 환경에서는 openstack server list에서 확인할 수 있다.

하지만 list로는 간단한 실행여부만 확인할 수 있기 때문에

openstack server show 서버이름으로 확인하면 어떠한 이유로 에러가 발생했는지 확인 할 수 있다.

```
 
