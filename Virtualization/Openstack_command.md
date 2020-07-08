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

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_envirment_credential_create.png" alt="drawing" width="700"/>

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
  
