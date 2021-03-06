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

## 레플리카셋

### 레플리카셋 소개

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_rs_yaml.png" alt="drawing" width="500"/>

+ 레플리케이션과 기본적인 철학과 방법은 같다.

+ 레플리케이션컨트롤러와 다른점은 `matchlabels`인데 이것은 파드의 다중레이블을 지원한다는것이다.

+ 또 하나의 기능은 파드에 설정된 레이블의 키만 선택가능

+ 파드가 많아지고 하나의 레이블을 가지고 컨트롤러에 매칭하기가 어려워짐으로써 발전함

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_rs.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_rs_yaml_labels.png" alt="drawing" width="500"/>

+ 먼저 yaml파일로 `matchlabels`와 밑에 파드템플릿에 `label`을 같게 하면 rs가 잘 생성이 된다.
+ 하지만 `matchlabels`와 파드템플릿에 `label`을 다르게하면 생성단계에서 막힌다.
+ 이런식으로 해당하는 `label`만 가진 파드만 `matchlabels`에서 확인후에 생성하기 때문에 관리하기가 편할 것 같다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_rs_yaml_matchlabels.png" alt="drawing" width="500"/>

+ 이런식으로 잘 작동한다.

### 디플로이먼트

+ 디플로이먼트는 파드와 레플리카셋에 대한 선언적 업데이트를 제공한다.

+ 디플로이먼트에서 의도하는 상태를 설명하고, 디플로이먼트 컨트롤러는 현재 상태에서 의도하는 상태로 비율을 조정하며 변경한다. 새 레플리카셋을 생성하는 디폴로이먼트를 정의하거나 기존 디플로이먼트를 제거하고, 모든 리소스를 새 디플로이먼트에 적용 할 수 있다.

+ **디플로이먼트가 소유하는 레플리카셋은 관리하지 말아야한다. 사용자의 유스케이스가 다음에 포함되지 않는 경우 리포지터리에 이슈를 올릴 수 있다.**

#### 유스케이스

+ 레플리카셋을 롤아웃 할 디플로이먼트 생성, 레플리카셋은 백그라운드에서 파드를 생성한다, 롤아웃 상태를 체크해서 성공여부를 확인한다.

+ 디플로이먼트의 PodTemplateSpec을 업데이트해서 파드의 새로운 상태를 선언한다. 새 레플리카셋이 생성되면, 디플로이먼트는 파드를 기존 레플리카셋에서 새로운 레플리카셋으로 속도를 제어하며 이동하는 것을 관리한다. 각각의 새로운 레플리카셋은 디플로이먼트의 수정 버전에 따라 업데이트한다.

+ 만약 디플로이먼트의 현재 상태가 안정적이지 않은 경우 디플로이먼트의 이전버전으로 롤백한다. 각 롤백은 디플로이먼트의 수정 버전에따라 업데이트한다.

+ 더 많은 로드를 위해 디플로이먼트의 스케일 업

## 데몬셋
### 데몬셋 소개
+ 노드 레이블과 매칭이 되는 모든 노드 또는 노드 레이블리 없다면 모든 노드에 하나씩의 파드를 동작시키는 컨트롤러이다.
+ 노드가 추가되면 자동으로 컨트롤러는 하나의 파드를 배치하게됨
+ 복제본 컨트롤러가 아니기 때문에, 노드가 제거되면 삭제된 파드를 다른 노드에 배치하지않음

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_ds_yaml.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_ds_labels.png" alt="drawing" width="500"/>

+ 데몬셋을 yaml파일로 설치를 해도 파드는 생성되지않는상태이다.
+ 왜냐하면 노드에 `label`이 없기때문이다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_ds_add_labels.png" alt="drawing" width="500"/>

+ `kubectl label nodes 노드이름 데몬셋에 추가한 레이블` 명령어로 노드에 레이블을 추가한다.
+ `kubectl get nodes --show-labels` 명령어로 노드들에 레이블이 추가되었는지 확인한다.
+ `kubectl get daemonsets.app` 로 데몬셋으로 생성된 파드가 있는지 확인한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_ds_delete_labels.png" alt="drawing" width="500"/>

+ `kubectl label nodes kube-node3 node-` 명령어로 노드에 레이블을 삭제한다.
+ `kubectl get daemonsets.app` 로 데몬셋에 파드가 있는지 확인한다.
+ 이처럼 노드에 해당하는 레이블이 없으면 파드도 없어진다.

## 잡
### 잡 소개
+ 잡 컨트롤러는 파드의 애플리케이션의 실행이 완료되는것에 초점을 맞춘 컨트롤러
+ 레플리케이션, 레플리카셋, 데몬셋이 파드의 어플리케이션이 계속해서 잘 작동하는 것에 초점을 맞춘것에 대비
+ 애플리케이션이 실행되고 실행이 완료되면 파드의 할 일이 끝난 것으로 간주하고 파드를 종료시킴
+ 잡 컨트롤러는 임시작업 및 배치작업에 유용하게 사용됨
+ 만약 애플리케이션 실행되고 있는 중에 노드가 죽거나 파드의 실행이 완료되지않았다면, 파드를 다시 스케쥴링하여 재실행하게 구성 할 수 있다.

### 잡 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_job_create_yaml.png" alt="drawing" width="500"/>

+ `kubectl apt-resources | grep job` 으로 apigroup을 확인한다.
+ `kubectl apt-versions | grep batch` 로 버전을 확인후에 yaml파일을 생성단계에 job에 apiVersion을 넣어준다.
+ `job`파일은 한번만 실행하는 파일이기때문에 spec에 재시작정책에 OnFailure(실패시 재시작:정상 종료시 재시작안함)를 넣어준다.
+ 이 `job`파일은 sleep상태로 60초동안 있다가 끝나면 완료상태로 변하는 파일이다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_job_complete.png" alt="drawing" width="500"/>

+ 생성하고 60초를 기다리고 다시 파드 상태를 확인했더니 complete상태로 변했다.
+ 이 `job`파일은 할일은 다하고 종료했다는 뜻이다.

## 크론잡

### 크론잡 소개
+ 잡 컨트롤러는 잡이 한번만 실행되지만 크론잡컨트롤러는 주기적으로 잡을 반복적으로 실행할 필요가 있을때 사용하는 컨트롤러이다.
+ 리눅스에 crontab기능과 같다.

### 크론잡 컨트롤러 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_cronjob_create_yaml.png" alt="drawing" width="500"/>

+ 크론잡리소스에 apigroup은 잡과 동일하게 batch이지만 버전이 `vibetav1`이다.
+ 잡이랑 다른것은 `schedule` 인데 리눅스에 crontab처럼 언제 실행할지 정하는 명령어 `분, 시, 일, 월, 요일`
+ 나머지는 job과 동일하다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_cronjob_watch.png" alt="drawing" width="500"/>

+ `CronJob` 파드의 상태를 확인
+ `cronjobs.batch`로 확인했더니 cronjob은 실패했다고 뜬다.
+ `kubectl get pods --watch` 실시간으로 확인했더니 실패하고 바로바로 다시 생성된다는걸 볼 수 있다.

### 크론잡 컨트롤러의 제한사항 소개
+ 크론잡 컨트롤러는 특정 스케줄링된 시간마다 하나의 잡을 실행한다.
+ 특정환경에서 잡이 실행되지 않거나 잡이 두개 이상 실행되는 경우도 있을 수 있다.
+ 이를 제어하기 위해 크론잡 컨트롤러의 잡이 제한사항을 설정 할 수 있다.

#### cronjob.spec.startingDeadlineSeconds : 시작 데드라인 시간
+ 초: 어떤 이유든 예정된 잡 시간시간에 대한 데드라인
  + 100초: 지금으로 부터 100초 안에 일정을 놓친 잡이 있는지 확인
 
#### cronjob.spec.concurrencyPolicy : 동시 실행 정책
+ allow: (기본) 잡이 동시에 실행 될 수 있음
+ forbid: 동시 실행 금지, 잡이 아직 완료되지 않은 경우 다음 잡은 건너뜀
+ Replace: 현재 실행중인 잡을 취소하고 새 잡으로 교체
