# Ansible

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_logo.png" alt="drawing" width="800"/>



## Ansible 이란?
`ref. https://docs.ansible.com/ ` 

`Ansible` 은 에플리케이션을 원격 노드에 배포하고 반복적으로 서버를 프로비저닝하는데 사용되는 오픈소스 도구


마스터-클라이언트 구조로 사용 할 수도있지만 푸시 모델 설정을 사용하여 다중 계층 응용프로그램 및 응용프로그램 아티팩트를 푸쉬하기 위한 공통 프레임워크를 제공함


`Ansible` 의 주요목표는 **단순성과 사용 편의성**이다. 또한 보안과 안정성에 중점을 두고 있으며 부품이동의 최소화, 전달을 위한 OpenSSH이 사용, 프로그램에 익숙하지 않은 사람까지도 이해하기 쉽도록 설된 언어를 포함한다.


`Ansible` 은 에이전트 없이 시스템을 관리한다. 원격 데몬을 업그레이드하는 방법이나 데몬이 제거돼 시스템을 관리 할 수 없는 문제에 대한 질문은 없다. OpenSSH는 가장 많이 검토된 오픈 소스구성 요소중 하나이므로 보안노출이 크게 줄어든다.
Ansible은 분산돼있으며 기존 OS 자격 증명을 사용하여 원격 컴퓨터에대한 엑세스를 제어한다. Kuberos,LDAP, 중앙 집중식 인증관리 시스템과 쉽게 연결가능하다.


`Ansible`은 매년 약 3-4회 Ansible의 새로운 주요버전을 release한다. 핵심 응용 프로그램은 언어 설계 및 설정의 단순성을 평가하면서 보수적으로 발전중이다. 하지만 새로운 모듈, 플로그인 개발에 대한 커뮤니티는 활발하게 움직이며 각 release에 많은 새로운 모듈에 추가한다.



#### Ansible의 장점

+ `SSH` 기반이므로 원격 노드에 에이전트를 설치할 필요가 없다.

+ `Yaml` 언어를 사용하기 때문에 쉽게 배울수 있다.

+ 플레이북 구조는 간단하고 명확하게 구조화되어 있다.

+ 변수 기능을 사용하여 같은 작업에 대해서 다른 구성으로 쉽게 구성 할 수 있다.

+ 다른 도구보다 훨씬 간소화 된 코드 기반이다.
 
 
  
#### Ansible의 단점

+ 다른 프로그래밍 언어를 기반으로 하는 도구보다 덜 강력합니다.

+ DSL(Domain Specific Language)을 통해 로직을 수행한다. DSL은 학습할 때까지 문서를 자주 확인하는것을 의미한다.

+ 변수 등록은 기본적인 기능조차도 요구되기 때문에 더 쉬운 작업을 더 복잡하게 만들 수 있다.

+ 플레이 내 변수의 값을 확인하기가 어렵다.
 
***
 
## Ansible architecture

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_architecture.png" alt="drawing" width="700"/>

**`Ansible`은 클라우드 프로비저닝, configuration 관리, 어플리케이션 배포, 인프라-서비스 오케스트레이션 및 여러 기타 IT 요구사항을 자동화 하는 IT자동화 엔진**

`Ansible`은 처음부터 Multi-tier 배포를 위해 설계되었으므로 한 번에 하나의 시스템을 관리하는 것이 아니라 모든 시스템이 상호 관련되는 방식을 설명함으로써 IT인프라를 모델링한다.
에이전트를 사용하지 않고, 추가적인 커스텀 보안 인프라또한 사용하지 않으므로 배포가 매우 쉽다. 가장 중요한 것은 간단한 언어인 `YAML`을 사용해 자동화 작업을 설명 할 수 있다.


### Controll Node

**`Ansible` 이 설치된 모든 시스템**

어떤 제어 노드에서든 `/usr/bin/ansible` 또는 `usr/bin/ansible-playbook` 호출함으로써 command 와 playbook 을 실행 할 수 있다. 랩탑, 데스크탑, 서버는 모두 python 만 설치되어있다면 모두 컨트롤 노드가 될 수 있다. 단, Window 시스템을 제어노드로 둘 수는 없고 제어노드를 가지는것은 가능하다.

### Managed nodes

**`Ansible`로 관리하는 네트워크장치**

관리되는 노드는 호스트라고도 한다. 관리하는 노드에는 `Ansible`이 설치되어있지 않다.
 
### Inventory

**관리되는 노드의 목록**

Ansible은 관리되는 모든 기기를 원하는 그룹으로 묶는파일을 가지고 관리하는 기기를 나타낸다. 새 시스템을 추가하기 위해 추가적인 SSL 서명 서버가 필요하지 않으므로 NTP 또는 DNS문제로 인해 특정 시스템이 연결되지 않는 번거로움이 없다.

인벤토리 파일은 때때로 호스트 파일이라고 한다. 인벤토리는 관리되는 노드에 대한 각각의 IP주소와 같은 정보를 지정 할 수 있다. 또한 인벤토리는 관리 노드를 구성하여 쉽게 확장 가능하도록 그룹을 만들고 중첩 시킬 수 있다.

일반적으로 인벤토리 파일의 구성
`
[webservers]
www.node1.com
www.node2.com

[dbservers]
db.node1.com
db.node2.com
`
인벤토리 호스트가 나열되면 변수는 간단한 텍스트 파일로써 이에 할당 될 수 있다. 동적 인벤토리를 사용해 EC2, Rackspace, OpenStack과 같은 데이터소스에서 인벤토리를 가져온다.

### Modules

**`Ansible` 코드의 실행 단위**

`Ansible`은 노드에 연결하고 `Ansible modules`라는 스크립트를 푸시함으로써 움직인다. 대부분의 모듈은 원하는 시스템의 상태를 설명하는 파라미터를 승인한다. 기본적으로 SSH를 통해 `Ansible`은 이러한 모듈을 실행하고, 완료되면 제거한다. 모듈 라이브러니는 모든 시스템에 상주 할 수 있으며, 서버 daemon, DB가 필요하지 않다.

자신만의 모듈을 작성 할 수 있지만 반드시 그럴 필요가 있는가에 대해 우선 고민해야한다. 일반적으로 자주 사용하는 터미널 프로그램, 텍스트 편집기 및 버전 제어 시스템을 사용해 컨텐츠 변경사항을 추척한다. JSON을 반환할 수 있는 모든 언어(Ruby, Python, bash, etc)로 특수 모듈을 작성해야 할 것이다.

각 모듈은 특정 유형의 데이터베이스에서 사용자를 관리하는것부터 특정 유형의 네트워크 장치에서 VLAN 인터페이스 관리까지 특정한 용도로 사용된다. 작업으로 단일 모듈을 호출하거나, 플레이북에서 여러 다른 모듈을 호출 할 수 있다.
 

### Plugins

`Plugin`은 Ansible의 핵심 기능을 강화한다. 모듈이 대상 시스템에서 별도의 프로세스로 실행되는 반면, 플러그인은 `/usr/bin/ansible/` 프로세스 내의 제어노드에서 실행된다. 플러그인은 데이터 변환, output로깅, 인벤토리 연결 등 Ansible의 핵심기능에 대한 옵션과 확장을 제공한다.

Ansible에서 여러 편리한 플러그인이 포함되어 있으며 쉽게 작성 할 수 있다. 인벤토리 플러그인을 작성하여 JSON을 반환하는 모든 데이터소스에 연결 할 수 있다. 플러그인은 Python으로 작성해야 한다.

### Tasks
**`Ansible` 의 작업단위**

`ad-hoc` 명령을 사용하여 단일 작업을 한 번 실행가능

### Playbooks

**반복해서 실행하고자 해당 작업을 실행 순서대로 저장해 놓은 정렬된 작업리스트**

플레이북에는 task 뿐만 아니라 변수도 포함 될 수 있다. 플레이북은 YAML로 작성돼있으며 읽거나 쓰거나 공유함

***




## Ansible 기본

### 1. 원격접속

SSH 키를 사용해서 호스트에 핑을 보내려면 controller에서 ssh로 노드들에 먼저 접속을해서 인증키를 가지고 있어야한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_hosts.png" alt="drawing" width="500"/>

인증키를 만든후에 `/etc/ansible/hosts` 에 ip주소와 도메인 정보를 넣어주어야 핑이 간다.

### 2. 키 인증 접속

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_key.png" alt="drawing" width="500"/>

공개키를 만들고 host마다 `ssh-copy-id ip주소`로 공개키를 복사한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_ping.png" alt="drawing" width="500"/>

복사하고서 `ansible all -m ping`으로 핑이 잘 작동하는지 확인한다.

### 3. 인벤토리 관리

Ansible은 인벤토리 파일에 나열된 시스템을 기준으로 작업을 수행한다.

파일은 기본적으로 `/etc/ansible/hosts` 이고 명령줄에 `-i` 로 직접 파일을 지정 할 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_inventory_list.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_graph.png" alt="drawing" width="500"/>

기본 리스트 파일형식에는 `그룹`으로 분류가 되는데 그룹을 따로 선언하지 않은 상태에서 작성한다면 `ungrouped`로 그룹이 없는상태로 분류된다.

`ansible-inventory -i 파일명 --list --yaml` 으로 지정된 파일에 형식을 볼 수 있는데

기본적으로는 `JSON`형식으로 보여주고 `yaml`파일 과 `graph`형식으로도 볼수 있다. 그래프형식에서는 그룹은 `@`으로 분류되어진다.

### 4. 패턴

`Ansible` 의 패턴은 관리 할 호스트를 결정하는 방법이다. 호스트가 통신 할 수 있는 것을 의미 할 수 있지만 플레이북의 관점에서 볼 때 실제로 호스트가 특정 구성이나 IT프로세스를 적용하는것을 의미한다.

Ad-Hoc 의 기본형식 `ansible <pattern_goes_here> -m <module_name> -a <argument>` 

Ad-Hoc 명령의 사용 예 `ansible webservers -m service -a "name=httpd state=restarted"`

### 5. Ad-Hoc 명령

`ref."https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_doc.png"`

위에 출처에서 `ansible` 모듈명령어를 볼 수 있다. 밑에 cli 환경에서도 `ansible-doc 명령어` 명령어를 볼 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_doc.png" alt="drawing" width="500"/>


#### copy

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_copy.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_copy_hosts.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_copy_result.png" alt="drawing" width="500"/>

`copy` 라는 명령어로 컨트롤러노드에서 노드1로 파일을 복사할수 있다. 경로는 절대경로로 지정해주어야 한다.
`controller 노드` 에 있는 `hosts`에 있는 정보를 노드들에 

#### file

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_file.png" alt="drawing" width="500"/>

`file`이라는 명령어로 노드들에 파일이 존재하는지 확인 할 수 있다. `state=absent`는 지금 파일이 없는 상태여야만 `Success`로 된다.

#### user

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_user.png" alt="drawing" width="500"/>

`user` 라는 명령어로 노드에 실행을 시키는데 유저를 만들기위해서는 `sudo`권한이 필요한데 권한이 없는 상태이다. 그래서 권한이 상승할 수 있도록 `-become, -b`로 해당 실행하는 유저에 sudo권한을 부여할 수 있고 sudo에 비밀번호를 넣을 수 있도록 도와주는 명령어는 `-K`이다
`state=present`는 해당 유저가 없다면 생성하는 명령어 반대로 `state=absent`는 있다면 삭제하는 명령어이다.

#### yum

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_yum_httpd.png" alt="drawing" width="500"/>

`yum`명령어와 `name=설치할패키지` 와 `state=installed` 

***

### 6. 구성파일

`ansible`의 특정 설정은 구성 파일을 통해 조정 할 수 있다. 변경사항은 다음 순서로 처리되는 구성파일에서 만들어 사용 하고 디렉토리마다 설정파일이 있다면 해당 디렉토리에 config파일로 적용되어 사용된다.

+ ANSIBLE_CONFIG

+ ansible.cfg (현재 디렉토리)

+ .ansible.cfg (홈 디렉토리)

+ /etc/ansible/ansible.cfg

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible-config.png" alt="drawing" width="500"/>

`ansible-config` 로 ansible 적용중인 설정파일들을 세가지 옵션으로 볼 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_configfile.png" alt="drawing" width="500"/>

새로운 `ansible config` 홈디렉토리에서 적용할 수 있는 설정파일을 생성하였다. `inventory`를 지정해서 `ansible` 명령에서 더이상 따로 지정하지 않아도 적용된다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_configview.png" alt="drawing" width="500"/>

`view` 는 현재 기본적으로 적용되는 파일들을 설명한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_configview_new.png" alt="drawing" width="500"/>

`view` 지금 사용하고 있는 설정파일로 보여준다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_configlist.png" alt="drawing" width="500"/>

`list`는 설정파일에 적용할때 방법을 설명한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_configdump.png" alt="drawing" width="500"/>

`dump`는 설정파일들이 어떠한 상태인지 볼 수 있다. 

***

## 플레이북

`Ansible-playbook` 으로 워드프레스 설치해보려고 한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_yaml_apache.png" alt="drawing" width="500"/>

`-hosts: apache` 아파치를 설치하고 워드프레스를 구성할 노드에 이름을 넣어준다.

`become: yes`은 설치하면서 `sudo`권한을 사용하는것을 따로 `-b`를 따로 부여하지않아도 허용한다.

`vars`로 변수를 선언 할 수 있다.

`remote_user`는 실행하는 유저에 이름을 넣어준다.

`tasks`는 실행 기본단위다. 한번의 모듈이 실행될때마다 `tasks`가 끝난다.

`yum`은 설치를 할 수 있는 모듈이다. `name`으로 설치할 패키지에 이름을 넣어주면 되고 `state`는 `latest`는 최신버전으로 설치한다.

`seboolean` 로 `selinux enforcing` 상태에서 http에서 데이터베이스를 접속 할 수 있는 권한만 허용해준다.

 이런식에 리스트형태로 모듈들로 명령어를 실행시킬 수 있다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_yaml_apache_exec.png" alt="drawing" width="500"/>
 
 모듈들이 문제없이 잘 작동된다면 ok만 나온다.
 
 문제가 생기는 `tasks`가 생긴다면 `failed`이 생기면서 문제원인을 알려준다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_yaml_db.png" alt="drawing" width="500"/>
 
 데이터베이스 설치하는 `Yaml`파일이고 제일 먼저 할일은 `yum_repository`에 데이터베이스 버전에 맞는 `repository`를 등록한다.
 
 그 후에 등록한 `repository`에 이름으로 인스톨을 시작한다. 설치가 완료되고 `mariadb`라는 시스템을 시작한다.
 
 이러한 방식으로 데이터베이스 생성과 사용자 생성 및 권한을 부여하며 워드프레스에서 접근하고 정보를 얻을 수 있는 데이터베이스를 설치했다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_yaml_wordpress.png" alt="darwing" width="500"/>
 
다시 `apache`서버의 ip주소로 접근하면 워드프레스가 잘 작동하고 사이트 제목만 입력하면 원하는 사이트를 구성할 수 있는 워드프레스가 구축되었다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_delete_apache_yaml.png" alt="drawing" width="500"/>

`wordpress` 를 생성하는 순서에 반대로 삭제하려고한다. 제일먼저 `seboolean`을 처음설정으로 반환하고 `http service`를 중지시킨다.
그 후에 `httpd` 

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_delete_db_yaml.png" alt="drawing" width="500"/>
