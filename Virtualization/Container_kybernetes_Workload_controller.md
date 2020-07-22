# 워크로드 - 컨트롤러
## 라이브니스 프로브
+ 파드를 직접 수동으로 생성, 모니터링, 삭제 등 관리하는 방법을 살펴보았다.
+ 실제환경에서는 수동으로 개입하지 않더라도 항상 정상적이고 안정적인 상태가 유지되기를 바람
+ 쿠버네티스 시스템은 이런 바람에 부합하게 동작하려면 라이브니스 프로브를 사용해야한다.

### 라이브니스 프로브 소개
+ 라이브니스 프로브는 파드에의해 컨테이너를 동작시키고 동작하고 있는 컨테이너가 잘 동작하는지 주기적으로 모니터링한다.
+ 만약 모니터링 도중 파드의 오류가 발생한다면 해당 컨테이너를 재시작
+ **라이브니스 프로브는 세가지 메커니즘을 가지고 컨테이너상태를 모니터링**
+ HTTP GET 프로브
  + 특정 경로에 HTTP GET 요청
  + HTTP 응답코드가 2XX 또는 3XX 인지 확인 함
+ TCP 소켓 프로브
  + 특정 TCP 포트연결을 시도함
+ Exec 프로브
  + 컨테이너 내부의 바이너리를 실행하고 종료 코드확인

### 라이브니스 프로브 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_liveness.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_liveness_httpd.png" alt="drawing" width="500"/>

+ ```livenessProbe```에서 HTTP GET프로브를 사용해서 체크하는 pod를 생성했다.
+ ```kubectl get pods --watch```로 생성된 pod를 체크할 수 있는지 확인해본다.


## 레플리케이션 컨트롤러
### 레플리케이션 컨트롤러 소개
+ 파드가 특정개수만큼이 복제되고 동작하는것을 보장한다.

+ 노드의 문제가 발생했거나 파드가 문제가 생겨 원하는 수의 파드가 동작하지 않는다면 자동으로 스케줄러에 의해 새로운 노드가 기존 노드에 다시 새로운 파드를 생성해 원하는 수의 파드를 복재해서 동작시킨다.

+ 파드가 원하는 수보다 많을 경우 원하는 파드수로 줄여준다(가장최근에 생성된 파드)

+ 셀랙터에 app과 템플릿 app은 반드시 같아야한다.

+ **원하는 수의 복제본 보다 더 많은 복제본이 많아 질수 있는 경우**
  + 수동으로 동일한 형식으로 파드를 생성
  
  + 기존의 파드의 유형을 변경
  
  + 원하는 수의 파드 복제본 수를 줄인 경우
  
+ **레플리케이션 컨트롤러를 구성하기 위해서는 세가지 요소가 있다.**
  + 파드를 지정하는 레이블셀렉터
  
  + 새로운 파드의 복제본을 만들기 위한 파드 템플릿
  
  + 복제본 수
  
+ **레플리케이션 컨트롤러가 제공하는 기능은 다음과 같음**
  + 원하는 복제본 수의 파드가 없는 경우 파드 템플릿을 이용하여 파드를 생성한다
  .
  + 노드에 장애가 발생하면 장애가 발생한 노드에서 실행 중이던 파드를 다른 노드에 복제본을 생성한다.
  
  + 수동이나 자동으로 파드를 수평 스케일링 할 수 있다.
 
### 레플리케이션 컨트롤러 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_replication_create.png" alt="drawing" width="500"/>

+ `kubectl create -f yaml파일명` 으로 replication도 생성할수있다
+ 기본적인 `replicas(유지할 pod수)` 는 3개로 정해서 3개가 생성되는것을 볼 수 있다.
+ `selector app` 과 `template app`이 같아야만 replication controller가 확인하고 유지할 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_replication_replace.png" alt="drawing" width="500"/>

+ replicas의 수를 yaml파일을 수정하고 실제 사용중인 쿠버네티스 rc를 수정하려면 `kubectl replace -f yaml파일명` 
