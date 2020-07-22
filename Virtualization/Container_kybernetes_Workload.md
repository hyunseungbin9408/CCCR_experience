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
***

## 참고 쿠버네티스 블로그
+ https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/
