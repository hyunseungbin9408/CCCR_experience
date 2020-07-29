# 쿠버네티스 디플로이먼트
## 디플로이먼트 어플리케이션 배포전략
### recreate
+ 오래된 버전을 종료시키고 새로운 버전을 릴리즈함

### ramped(rolling update)
+ 새로운버전을 하나씩 업데이트하는방법

### blue/green
+ 두가지의 버전을 가지고 하나만 네트워크를 연결해놓고 한 버전의 문제가 생기면 지난버전에 네트워크를 연결
+ 새로운 버전에 문제가 없다면 지난버전을 삭제함

### canary
+ 아주 적은 트래픽으로 새로운버전을 만들어놓고 새로운 사람들에게만 배포를 했다가 문제가 없으면 모든버전을 업데이트함

### A/B testing (쿠버네티스에선 구성할수없음)
+ 사용자들은 지난버전을 사용하는데 새로운버전에 트래픽을 보내보고 문제가 없으면 배포
+ 사용자들은 지난버전만 사용하기때문에 canary와는 다름

***

## 레플리케이션 컨트롤러 롤링 업데이트
+ 엡

## 디플로이먼트
### 디플로이먼트 정의


### 디플로이먼트 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Deployment_yaml.png" alt="drawing" width="500"/>

+ 디플로이먼트는 레플리카셋을 관리하는 컨트롤러이고 `rollingUpdate`가 필수적으로 들어간다.

+ `maxUnavailable`은 `Deployment`가 업데이트를 진행할때 최대 몇개를 한번에 삭제 할것인가 결정한다.

+ `maxSurge`는 업데이트를 진행할때 새로운 버전에 파드를 몇개 생성할지 결정한다.

+ `minReadySeconds` 업데이트를 할때 컨테이너가 다음 상황을 얼마나 대기할지 결정한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Deployment_history.png" alt="drawing" width="500"/>

+ `kubectl rollout history deployment`로 디플로이먼트가 버전기록을 볼 수가있다.

+ 이것도 우리가 디플로이먼트를 구성할때 `spec` 밑에 `revisionHistoryLimit` 로 몇개까지의 히스토리를 저장하고있을지 결정 할 수 있다.

+ 이러한 히스토리가 있어야만 `undo` 명령어로 이전 버전으로 돌아갈 수 있고 그만큼에 `ReplicaSet`을 가지고 있는것이다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Deployment_rollout.png" alt="drawing" width="700"/>

+ 디플로이먼트를 업데이트 하는방법은 `kubectl set image deployment 컨테이너이름 컨테이너이름=새로운이미지명` 으로 명령어를 입력한다.

+ `watch -n1 -d curl`로 실시간 응답이 오는지 확인하면 버전이 중간중간 바뀌는것을 알 수 있다.

+ 레플리카셋은 살펴보면 그전버전 컨트롤러가 아직 삭제되지 않은것을 알 수 있는데 이것은 `rollback`하는것을 위해서이다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Deployment_update_record.png" alt="drawing" width="700"/>

+ 업데이트하는 과정에서 `--record` 명령어를 추가로 입력하면 `history`에서 어떠한 명령어로 업데이트를 했는지 알 수 있다.
