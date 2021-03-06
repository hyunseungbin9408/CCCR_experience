# 오픈스택 Packstack Openstack 설치

## 실습 시스템설정

VM (Centos 7.8)

CPU: 4(Copy Host Configuration)
Memory: 10G
Nic: nat / private 1

ip대역

IP: 192.168.122.180/24, 192.168.123.180/24
GW: 192.168.122.1
DNS: 8.8.8.8 / 8.8.4.4

## 설치법

먼저 패키지를 모두 업데이트를 해준다.

` sudo yum -y update`

이때 커널이 업데이트가 되면 재부팅을 해줘야 한다.

` sudo reboot`

재부팅이 완료되면 

` sudo yum install -y centos-release-openstack-train`

으로 centos 버전 오픈스택 train을 설치하고

` sudo yum -y update`

다시한번 패키지를 업데이트해준다.

그 후에 오픈스택을 다운받을 수 있는 packstack패키지를 설치한다.

`sudo yum install -y openstack-packstack`

설치하면 packstack 명령어를 사용할 수 있다.

`packstack --gen-answer-file=answer.txt`

설치할때 문답하는 명령어들을 파일로 만들어보았다
몇백개이상에 문답이 있어서 하나하나 작성하기는 부담스럽다.

기본 호스트 주소와 오픈스택에 각 기능에 디폴트값도 들어가있다.

`CONFIG_CONTROLLER_HOST=192.168.123.180`

이러한 값들이 들어가있다.

`packstack --answer-file=answer.txt`

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/packstack_install.png" alt="drawing" width="700"/>


## kolla ansible install

`ref. https://docs.openstack.org/kolla-ansible/train/user/quickstart.html`

설치 순서는
+ python

+ (python virtual Environment)

+ ansible2.6~2.9

+ kolla-ansible (playbook for deploying openstack)

ansible 

kolla ansible 버전은 train을 설치

kolla ansible 을 다운받기 위해서는 기본적인 환경이 필요하기때문에 
다음과 같은 패키지를 설치

`sudo yum install python-devel libffi-devel gcc openssl-devel libselinux-python`

파이썬 가상환경을 사용 할 수 있는 패키지 설치

`sudo yum install python-virtualenv`

가상환경명령어에 경로를 정해주고
소스로 적용시키면 사용 할 수 있다.

`virtualenv /path/to/virtualenv
source /path/to/virtualenv/bin/activate`

ansible 
eth0 Internal  // 192.168.122.180/24
eth1 External  // IP를 수동으로 지정하면 안됌

os 
eth0 Internal // 192.168.122.181/24
eth1 External // IP를 수동으로 지정하면 안됌

가상환경에서 진행해야되고 root로 실행하면 폴더가 바껴서 진행이 안된다.

