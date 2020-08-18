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

