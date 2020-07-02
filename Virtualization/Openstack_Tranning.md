## 오픈스택 실습

### 1 ) Controller 서버

- Cpu 2코어
- Memory 8192
- **구성 노드**
- Controller
- Network
- Storage

### 2 ) compute 서버

- cpu 2
- Memory 4096
- **구성 노드**
- Compute

### Controller 서버 (admin관리자)

#### 1) 오픈스택 노드 상태 확인패키지 설치
```
yum -y install openstack-utils

→ 설치하면 openstack-status

 오픈스택 노드 상태 확인 커맨트 활성화
```
#### 2) 오픈스택 관리웹페이지 접속

```
 openstack-utils 를 설치하면 루트 디렉토리에
 answers.txt  keystonerc_admin 에 오픈스택관리자 계정정보가 들어가있다.
 
 
 우리는 프로젝트와 identity를 사용할 것이다.
 회사에서 각각 프로젝트를 할당 할 수 있다.

```
#### 3) 오픈스택 관리자 웹페이지 사용자 관리

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_usercreate.png" alt="drawing" width="400"/>

```
 인증탭에서 사용자를 클릭하고 생성 할 수 있다.
 이름과 암호를 입력해주고 원하는 프로젝트에 속하고 역할도 부여해 줄 수 있다. // 어느 한 프로젝트에 admin역할이 된다면 모든 프로젝트를 관리 할 수 있다.
 사용자에게 역할을 하나하나 부여할 필요없이 그룹묶어서 한꺼번에 역할을 부여해 줄 수 있다. 
 ```
#### 4) 오픈스택 관리자 시스템정보확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_systeminfo.png" alt="drawing" width="400"/>

```
 왼쪽상단 관리탭에서 시스템정보를 확인 할 수 있다. Endpoint로 주소를 확인 할 수 있는데 노드마다 주소가 각각 다르다.
```
#### 5) 오픈스택 관리자 flavor 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_flavor_create.png" alt="drawing" width="400"/>

```
flavor를 통해서 우리는 인스턴스 배포시에 RAM, 디스크, CPU 코어 수, 기타 리소스의 크기를 규정해 둘 수 있다.
우리가 생성하고 싶은 centos7 파일에는 기본적으로 8~9GB에 공간이 필요한데 
오픈스택에서 기본적으로 생성되어있는 flavor에는 딱 맞는것이 없어서 생성해야한다.
위에 보는것처럼 조금은 여유있게 만들었다. 타이트하게 만들면 생성시에 거부당 할 수 있기 때문이다.
```

#### 6) 오픈스택 관리자 이미지파일 공유파일로 등록

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_image_create.png" alt="drawing" width="400"/>

```
이미지 파일을 공용으로 등록해서 필요할 때마다 사용 할 수 있도록 생성하려고 한다.
관리자 계정으로 접속하고 이미지파일을 생성해야 공용으로 만들 수 있고 사용자계정으로 들어간다면 private(선택불가)으로 생성된다.
오픈스택 전용 iso파일을 다운받고 업로드 후에 포멧은 QCOW2파일형식으로 설정해준다.
이 iso파일은 기본적으로 최소 디스크8GB가 필요하니 스토리지는 8기가이상만 사용할 수 있도록 제한을 두어야 한다.
```

#### 7) 오픈스택 관리자 네트워크 생성 및 관리

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_public_network.png" alt="drawing" width="400"/>

```
 오픈스택 외부망을 생성하는 방법은 먼저 메뉴탭에 프로젝트 -> 네트워크 -> 네트워크생성 
 프로젝트는 남들에게 보여주지 않기위해서 admin 프로젝트를 선택해준다
 그 다음 네트워크 타입은 우리가 사용할 수 있는 flat으로 설정한다.
 설정하면 물리네트워크가 등장하는데 extnet으로 설정해준다.
 extnet이란것은 그랩으로 확인 할 수 있다.
 밑에 pools할당은 우리가 할당받는 ip주소의 범위를 정 할 수가 있다. " , " 로 범위를 정할 수 있다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_physicialnetwork_check.png" alt="drawing" width="400"/>

***

### 사용자 계정

#### 1) 프로젝트 내부망 네트워크 생성


<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_create2.png" alt="drawing" width="400"/>

```
 내부망을 설치하는 방법은 프로젝트메뉴에서 네트워크 -> 네트워크생성하면 
 네트워크 이름 후에 서브넷으로 넘어가서 서브넷 이름을 정해주고
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_create3.png" alt="drawing" width="400"/>

```

DNS서버를 정해주는 것이 좋다. // 8.8.8.8로 주소를 주었다.
```

#### 2) 프로젝트 라우터 생성

 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_create_topology.png" alt="drawing" width="40
 0">
 
```
 오른쪽 위에 라우트생성에 들어가서 이름을 넣고 라우트 생성후에 인터페이스를 연결해주면 라우트를 통해서 외부망과 내부망을
 연결한 네트워크가 완성되었다.
```

#### 3) 프로젝트 보안그룹 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create2.png" alt="drawing" width="400"/>

```
 프로젝트 메뉴탭에서 보안그룹으로 가면 기본적으로 생성되어있는 default라는 그룹이 있는데 이 그룹은
 모든 사용자에게 적용시킬 수 있다. 그래서 가상머신을 생성할때 기본적으로 들어가야하는 포트와 서비스를 입력해준다.
 인스턴스로 생성된 가상머신은 원격으로 접속해서 컨트롤하기 때문에 ssh가 필수이다. ssh를 뜻하는 22번 포트와
 네트워크가 제대로 적용되었는지 확인 할 수 있는 ICMP(ping)를 열어주면 된다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create3.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_securityGroup_create4.png" alt="drawing" width="400"/>


```
 우리는 워드프레스와 로드밸런스를 구성할 것이기때문에 웹을 구성하는 보안그룹을 만들어준다.
 웹을 구성할때 열어주어야하는 필수 포트 HTTP(80)과 HTTPS(443)을 열어주어야한다.
 이름을 구성하고 보안그룹을 생성하고 전에 했던것처럼 포트를 추가해준다.
```

#### 4) 프로젝트 Floating 

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_network_Floating.png" alt="drawing" width="400"/>

 ```
 외부망으로 통신 할 수 있도록 유동ip를 설정 할 수 있게 Floating 설정해준다.
 ```
 
#### 5) 프로젝트 컴퓨트 키페어 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_keypair_create.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_keypair_create_key.png" alt="drawing" width="400"/>

```
 컴퓨트 메뉴에서 키페어를 들어가 키페어를 생성할때 이름만 넣어주면되고 생성을 완료하면
 다운로드창이 등장하는데 그것은 개인키를 다운받는것이다. 
 우리는 키페어로 인스턴스를 생성 및 원격실행 할 것이기때문에 컨트롤러 노드에 .ssh폴더에 넣어준다.
 개인키이기때문에 권한을 600 사용자에게만 읽고 쓸수있는 권한을 준다.
```

#### 6) 프로젝트 인스턴스 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_instance_create.png" alt="drawing" width="400"/>

```
 인스턴스 생성을 처음 들어가면 이름을 설정해주고 소스로 넘어가면 된다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_instance_create_image.png" alt="drawing" width="400"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_instance_create_volume.png" alt="drawing" width="400"/>


```
 소스탭에서는 이미지파일을 등록하는것과 부트볼륨을 등록하는 것 두가지 방법이 있다.
 이미지 파일로 부트를 실행한다면 인스턴스를 만들때마다 새롭게 설정해야하고
 부트볼륨으로 소스를 등록하고 볼륨을 삭제하는것을 체크해제하면 볼륨안에 설정들을 그대로 가지고 갈 수 있다.
 ```
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_instance_create_flavor.png" alt="drawing" width="400"/>
 

```
 admin계정에서 생성했던 flavor을 등록하는 단계이다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_instance_security.png" alt="drawing" width="400"/>

```
 인스턴스에 보안그룹을 등록하여 방화벽을 관리하는 단계이다. default값은 기본적으로 들어가있고 추가로 설정한 보안그룹을 올려주면 끝이다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_instance_create_configuration.png" alt="drawing" width="400"/>

```
설정에서 나는 cloud init 스크립트로 워드프레스를 자동화로 다운 실행 할 수 있게 설정하였다.
이로써 인스턴스를 생성 할 수 있게 되었다.
```

#### 7) 프로젝트 로드밸런스

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_loadbalancer.png" alt="drawing" width="400"/>

```
 로드밸런스를 생성할때 로드밸런스를 시켜줄 대역에 서브넷을 정해준다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_loadbalancer2.png" alt="drawing" width="400"/>

```
로드밸런스로 접속할 포트를 정해준다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_loadbalancer3.png" alt="drawing" width="400"/>

```
 로드밸런스를 진행할 방식을 정한다.
 Round Robin은 분산은 순차적으로 실행한다. 제일 기본적인 방법
Least_connection은 초반에는 Round Robin처럼 순차적으로 진행하다가 트래픽이 제일 적은쪽으로 분산을 시켜주는 방법이다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_loadbalancer4.png" alt="drawing" width="400"/>

```
로드밸런싱을 진행할 대역폭에 속해있는 서버들을 골라서 넣을수있다.
포함시킨 서버들만 로드밸런싱이 들어간다.
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_loadbalancer5.png" alt="drawing" width="400"/>

```
모니터링을 어떤방식으로 진행 할지 정하는 단계이다. 모니터링 tcp를 http로 시키고 3번이상 5초동안 넘게 반응이 오지않는다면
해당서버에 로드밸런싱을 중지한다.
기본값으로 진행시켰다.
```
