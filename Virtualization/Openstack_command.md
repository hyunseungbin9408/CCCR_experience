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
