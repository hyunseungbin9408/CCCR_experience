# 워크로드(Workload)

## 파드
### 파드의 기본
 + 파드는 쿠버네티스 어플리케이션의 기본 실행 단위
 + 파드는 클러스터내에서 애플리케이션을 배포하며 동작하는 프로세스
 + 파드는 애플리케이션 컨테이너이고 하나 이상의 컨테이너로 구성됨
 + 쿠버네티스 클러스터 내부의 파드는 두 가지 방법으로 사용됨
   + 단일 컨테이너만 동작하는 파드
   + 다중 컨테이너가 동작하는 파드
 + 파드에 하나 이상의 컨테이너가 있다고 하더라도 파드의 컨테이너는 같은 노드에서만 동작
 + **하나의 파드는 하나의 컨테이너만 넣는것이 기본**

 
 
### 파드는 어떻게 다중 컨테이너를 관리하는가
+ 파드는 결합도가 있는 단위의 서비스를 형성하는 다중 협력 프로세스를 지원하도록 디자인 되어있음
+ 파드 내부의 컨테이너는 자동으로 동일한 물리적 또는 가상의 머신의 클러스터에 함께 배치되고 스케쥴된다.
+ 파드는 같은 파드안에 속한 컨테이너에게 두 가지 공유 리소스인 네트워킹과 저장소를 제공한다.
+ 파드안에는 몇개의 컨테이너가 있던지 같은 네트워크를 쓰기때문에 같은 포트를 열수가 없다.

### 멀티 컨테이너 파드 종류
#### Sidecar container는 주 목적의 컨테이너를 보조하기위한 보조 컨테이너들이 딸려오는것 (web)
+ 사이드카는 기능의 확장형태

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_sidecar.png" alt="drawing" width="500"/>

#### Ambassador containers
+ 네트워크 프록시 연결

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_ambassador.png" alt="drawing" width="500"/>

#### Adapter containers

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_adapter.png" alt="drawing" width="500"/>

#### 네트워킹
+ 각각의 파드는 각 주소 패밀리의 고유한 IP주소를 할당 받는다.
+ 한 파드 내부의 모든 컨테이너는 네트워크 네임스페이스와 IP주소 및 네트워크 포트를 공유한다.
+ 파드 안에있는 컨테이너는 다른 컨테이너와 Localhost를 통해서 통신 할 수 있다.
+ 특정 파드 안에 있는 컨테이너가 파드밖의 요소들과 통신하기 위해서는, 네트워크 리소르를 어떻게 쓰고있는지 공유해야함 (포트)

#### 저장소
+ 파드는 공유 저장소 집합인 볼륨을 명시 할 수 있다.
+ 파드 내부의 모든 컨테이너는 공유 볼륨에 접근 할수 있음
+ 컨테이너끼리 데이터를 공유하는것을 허용
+ 볼륨은 컨테이너가 재시작되어야 하는 상황에도 파드안의 데이터가 영구적으로 유지 될 수 있게한다.

***

### 파드 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_yaml.png" alt="drawing" width="500"/>

+ 먼저 파드를 생성할수있는 Yaml파일을 기본적인 정보만 넣어서 만들었다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_create.png" alt="drawing" width="500"/>

+ 파드를 생성하고 실행되는지 확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_yaml_check.png" alt="drawing" width="500"/>

+ 파드 정보를 Yaml 파일로 확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_describe.png" alt="drawing" width="500"/>

+ 파드에 대한 설명을 확인
+ **desribe 에서 제일 중요한 점은 events를 확인 할수 있다.**
+ events는 리소스들의 로그를 확인 할 수 있다.
+ events는 위에서 아래로 진행된다.


<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_logs.png" alt="drawing" width="500"/>

+ 파드에 로그를 확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_port_forwarding.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_pods_curl.png" alt="drawing" width="500"/>

```

kubectl port-forward mynapp-pod 8080:8080

호스트 포트를 컨테이너의 포트로 포워딩을 해주었다.

새로운 터미널에서 curl로 접근하면 접속할 수 있다.

```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_pods_exec.png" alt="drawing" width="500"/>

```
도커에서 컨테이너에 접근할때 했던것처럼

docker exec 로 컨테이너안에서 명령어를 실행 시킬수 있다.

```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_pods_create2.png" alt="drwaing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_pods_curl2.png" alt="drawing" width="500"/>

```

새로운 yaml 파일을 만들어서 새롭게 pods를 만들고 

포트포워딩을 해서 접속까지 해보았다.

```

### 레이블 및 셀렉터
#### 레이블 소개
+ 레이블은 pod를 분류하고 검색하기 위해서 사용한다.
+ 쿠버네티스 클러스터의 모든 오브젝트에 키/값쌍으로도 리소스를 식별하고 속성을 지정하는데 사용
+ 오브젝트 개수가 많아진다면 오브젝트를 식별하는데 매우 어려울 수 있다.
+ 오브젝트의 적절한 레이블을 부여하여 성격을 정의하고 검색을 용이하게 할 수 있다.
+ 레이블의 예
  + release: stable / canary / A / B
  + environment: dev/ qa / production
  + tier: frontend / backend / cache / database
  + partition: customerA / customerB
  + track: daily / weekly
  + app: webapp / middleware
 
#### 레이블 적용

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_label.png" alt="drawing" width="500"/>

```
 yaml파일 metadate에 label을 추가했다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_pods_label_add.png" alt="drawing" width="500"/>

```

 처음 pod를 생성할때도 추가할수있지만 이미 생성된 pod에도 추가할수 있다.
 
 kubectl label pods 파드이름 추가할 label
 
 로 추가하고 kubectl get 파드 --show-lables 레이블값
 
 레이블이 들어가있는것을 확인 할 수 있다.
 
 ```
***

## 볼륨
+ 컨테이너 내의 디스크에 있는 파일은 임시적이다.
+ 컨테이너에서 실행 될 때 애플리케이션에 적지않은 몇 가지 문제가 발생한다.
  + 첫째로 컨테이너가 충돌되면, kublet은 컨테이너를 재시작시키지만, 컨테이너는 깨끗한 상태로 시작되기 때문에 기존 파일이 유실된다.
  + 둘째로 pod에서 컨테이너를 함께 실행할때 컨테이너 사이에 파일을 공유해야 하는 경우가 자주 발생한다.
+ 쿠버네티스의 볼륨 추상화는 이 두가지 문제를 모두 해결한다.

### 배경
#### 도커볼륨
+ 도커는 다소 느슨하고, 덜 관리되지만 볼륨이라는 개념을 가지고 있다.
+ 도커에서 볼륨은 단순한 디스크 내 디렉터리 또는 다른 컨테이너에 있는 디렉터리다.
+ 수명은 관리되지 않으며 최근까지는 로컬 디스크 백업 볼륨만 있었다.
+ 도커는 이제 볼륨 드라이버를 제공하지만, 현재 기능은 매우 제한되어 있다.

#### 쿠버네티스 볼륨
+ 쿠버네티스 볼륨은 그것을 둘러싼 파드와 동일한 명시적인 수명을 가진다.
+ 그 결과로 볼륨은 파드 내에서 실행되는 모든 컨테이너보다 수명이 길고, 컨테이너를 다시 시작해도 데이터가 보존된다.
+ 물론 파드가 존재하지 않으면, 볼륨도 존재하지 않는다.
+ 이보다 더 중요한 것은 쿠버네티스가 많은 유형의 볼륨을 지원하고 파드는 여러 볼륨을 동시에 사용 할 수 있다.
+ 기본적으로 볼륨은 디렉터리일 뿐이며, 일부 데이터가 있을 수 있다.
+ 파드 내 컨테이너에서 접근 할 수 있다.
+ 디렉터리 생성방식, 이를 지원하는 매체와 내용은 사용된 특정볼륨의 유형에 따라 결정된다.
+ 볼륨을 사용하기 위해 파드는 파드에 제공할 볼륨과 컨테이너에 마운트할 위치를 지정한다.
***

## 참고
+ 쿠버네티스 공식홈페이지 (https://kubernetes.io/ko/docs/concepts/storage/volumes/)
+ 쿠버네티스 공식 블로그 (https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/)
