# Wordpress 구성하기

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_trainning_7.3.png" alt="drawing" width="700"/>

+ DB서버에서 마운트 포인트 (/var/lib/mysql)
+ WEB서버에 마운트 포인트 (/var/www)

## 실습 목표
 1. 기본적인 네트워크 구성
 2. Web서버 구축 및 Wordpress 구성
 
## 오픈스택 구성

### web 서버 인스턴스

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_training_web.png" alt="drawing" width="500"/>

 + 웹서버에 실행파일은 부트볼륨으로 하지않고 왜냐하면 총 사용할 수 있는 공간이 20GB밖에 없어서 효율적 공간사용하려고 이미지파일로 직접 구동했다.
 + 보안그룹은 mysql(3306), http(80), https(443)이렇게 세개로 기본값에 더해서 추가 해주었다.
 + 
