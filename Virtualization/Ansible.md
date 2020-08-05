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



### Ansible의 장점

`SSH` 기반이므로 원격 노드에 에이전트를 설치할 필요가 없다.

`Yaml` 언어를 사용하기 때문에 쉽게 배울수 있다.

플레이북 구조는 간단하고 명확하게 구조화되어 있다.

변수 기능을 사용하여 같은 작업에 대해서 다른 구성으로 쉽게 구성 할 수 있다.

다른 도구보다 훨씬 간소화 된 코드 기반이다.
 
 
  
### Ansible의 단점

다른 프로그래밍 언어를 기반으로 하는 도구보다 덜 강력합니다.

DSL(Domain Specific Language)을 통해 로직을 수행한다. DSL은 학습할 때까지 문서를 자주 확인하는것을 의미한다.

변수 등록은 기본적인 기능조차도 요구되기 때문에 더 쉬운 작업을 더 복잡하게 만들 수 있다.

플레이 내 변수의 값을 확인하기가 어렵다.
 
 
 
## Ansible 용어

`Ansible`을 학습하기 위해 기본적으로 알아야하는 용어들

+ **컨트롤 머신**
 
 
 
## Ansible architecture

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_architecture.png" alt="drawing" width="700"/>


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

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_copy.png" alt="drawing" width="500"/>

`copy` 라는 명령어로 컨트롤러노드에서 노드1로 파일을 복사할수 있다. 경로는 절대경로로 지정해주어야 한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_file.png" alt="drawing" width="500"/>

`file`이라는 명령어로 노드들에 파일이 존재하는지 확인 할 수 있다. `state=absent`는 지금 파일이 없는 상태여야만 `Success`로 된다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ansible_user.png" alt="drawing" width="500"/>

`user` 라는 명령어로 노드에 실행을 시키는데 유저를 만들기위해서는 `sudo`권한이 필요한데 권한이 없는 상태이다. 그래서 권한이 상승할 수 있도록 `-become, -b`로 해당 실행하는 유저에 sudo권한을 부여할 수 있고 sudo에 비밀번호를 넣을 수 있도록 도와주는 명령어는 `-K`이다
`state=present`는 해당 유저가 없다면 생성하는 명령어 반대로 `state=absent`는 있다면 삭제하는 명령어이다.

