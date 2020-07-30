# 쿠버네티스 파드 스케줄러
## 노드네임
+ 파드 스케줄러를 사용하지 않는 방법: 노드네임
+ 파드 스케줄러를 사용하는 방법: 노드 셀렉터, 어피니티, 테인트, 톨러레이션, 커든, 드레인

+ 노드네임 기능을 추천하지않는 이유
  + 지정된 노드가 존재하지 않으면 파드가 실행되지 않거나 컨트롤러에 의해 삭제 될 수 있다.
  + 지정한 노드의 리소스가 충분히 없는 경우, 파드가 생성이 실패함
  + 클라우드 환경에서 노드의 스케일링에 따라 노드 이름이 변하거나 고정되지 않는다.
 
### 노드네임을 이용해서 리소스 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_nodename_yaml.png" alt="drawing" width="500"/>

+ 기본 레플리카셋에 `template.spec`에 특정한 노드에 이름으로 지정가능

+ 이 레플리카셋에서 생성되는 파드는 해당 노드에서만 생성가능
  
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_nodecheck.png" alt="drawing" width="500"/>

## 노드 셀렉터
+ 노드셀렉터는 파드를 특정 노드에 배치하기 위해 파드 스케줄러를 제어하는 가장 쉬운 방법
+ 노드 셀렉터는 노드에 레이블을 지정하고, 컨트롤러 및 파드 선언시 `.spec.nodeSelector`필드로 레이블을 이용해 노드를 선택

### 노드 레이블 설정

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_nodelabels.png" alt="drawing" width="500"/>

+ 각 노드에 레이블을 설정 할 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_nodeselector_yaml.png" alt="drawing" width="500"/>

+ 노드 셀렉터는 노드에 지정된 레이블로 생성하는 파드의 노드들을 정할 수 있다.

## 어피니티

+ 어피니티라는것은 선호도를 뜻한다.

+ 노드네임 또는 노드 셀렉터는 특정 파드를 배치 할때 특정 노드를 정확히 지칭하지만 어피니티는 선호하는 노드의 엄격함을 지정할 수 있다.

+ 특정노드에 배치되는 것을 선호하지만 반드시 따라야하는 룰은 아닐수도 있다는 의미다.

+ 파드간에도 선호도와 비-선호도를 지정해 같은 노드에 배치 될것이냐, 다른 노드에 배치 될 것이냐를 지정 할 수 있다.

+ 자주 통신하는 파드사이에는 같은 노드에 배치되게 하고, 리소스를 많이 사용하는 파드들은 같은 노드에 배치되지 않도록 하는 방법

+ **어피니티 종류**
  + 노드어피니티: 파드를 특정 노드에 배치 할 것을 선호
  
  + 파드 어피니티: 파드간에 같은 노드에 배치 할 것을 선호
  
  + 파드 안티 어피니티: 파드간에 다른 노드에 배치 할 것을 선호
  
### 노드 어피니티
+ 노드 어피니티는 노드 셀렉터와 비슷하게 파드를 특정 노드에 배치 할 수 있다.

+ 노드 셀렉터는 해당 레이블이 있는 노드에만 배치되지만, 노드 어피니티는 파드의 배치를 특정 노드에 강제하지 않을 수 있다.

+ 파드를 생성할때 어피니티는 `preferrend`를 에매해서 쓰지않는다.

#### 노드 어피니티 오브젝트

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_affiniti_yaml.png" alt="drawing" width="500"/>

+ `requiredDuringSchedulingIgnoredDuringExecution:`는 스케줄링을 할때에는 요구하지만 실행할때에는 무시한다는 명령어

+ 이 파드가 생성될때에는 이러한 레이블들을 요구해서 파드를 생성함

+ 실행될때에는 영향을 미치지 않는다.

+ `preferredDuringSchedulingIgnoredDuringExecution:`는 스케줄링을 할때에 이러한 값들을 다른값들보다 더 선호한다는 명령어

+ 파드 생성할때에는 에매한 점이 있어서 쓰지않는다.

### 파드 어피니티 및 안티 어피니티
+ 파드 어피니티 및 안티 어피니티는 파드간에 같은 노드에 배치 할것인지, 다른 노드에 배치할 것인지 선호도를 지정할 수 있다.

+ 웹을 구성할때 ` podaffinity`는 캐쉬와 프론트엔드를 같은 노드에 배치하도록 한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_podaffiniti_cache_yaml.png" alt="drawing" width="500"/>

+ 웹을 구성할때 캐쉬에 대한 파드를 생성하는 파일

+ `podAntiAffinity:` 는 파드끼리 같은 노드에 속하지 않도록 비-선호한다는 뜻이다.

+ 캐쉬라는것을 같은 노드에 저장하면 의미가 없어지기때문에 각가 다른 노드에 배치를 하려고하는것

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_podaffiniti_fronted_yaml.png" alt="drawing" width="500"/>

+ 캐쉬파드를 노드에 각각 존재하게 했고 프론드엔드 파드도 노드마다 한개씩 존재하도록 만들었다.

+ `podAffinity:`는 어떠한 파드를 같은 노드에 배치할지 결정하는 명령어이다.

+ 같은 노드에 프론트엔드파드와 캐쉬파드가 동시에 존재하도록 할 수 있는 명령어이다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_podaffiniti_get.png" alt="drawing" width="500"/>

+ `yaml`파일로 캐쉬와 프론트엔드를 생성했고 어느 노드에 배치되었는지 확인

+ 캐쉬파드들끼리 다른노드로 배치되었고 프론트엔드들도 다른노드에 배치

+ 프론트엔드와 캐쉬파드 한쌍으로 묶여있는것을 확인

## 테인트 및 톨러레이션

+ 테인트는 쿠버네티스 클러스터의 특정 노드에 더이상 추가적인 파드가 배치되지 않도록 파드를 스케줄링 하지않는다.

+ 톨러레이션을 사용하면 테인트가 설정된 노드에 파드를 스케줄링 할 수 있도록 구성

+ **테인트와 톨러레이션을 사용하는 주요목적은 쿠버네티스 클러스터의 노드에 특정 역할을 할당하기 위해 사용한다.**

+ 노드에 GPU가 있고, GPU를 사용하지 않는 애플리케이션 파드는 배치하지않고 GPU를 사용하는 애플리케이션은 해당 노드에 배치

+ 쿠버네티스 클러스터의 마스터 노드에는 마스터 역할의 테인트를 부여했기 때문에 특정 톨러레이션이 없는 경우 마스터 노드에 스케줄링 하지않는다.

### 테인트

+ ` kubectl taint [NODE] [NODE-NAME] [KEY=VALUE:EFFECT] ...` 처럼 설정한다.

+ **테인트의 효과는 세가지**
  + NoSchedule: 톨러레이션에 해당 레이블이 없는 파드는 스케줄링 할 수 없다. (기존 파드에 적용되지 않음)
  
  + PreferNoSchedule: 톨러레이션에 해당 레이블이 없는 파드는 스케줄링 할 수 없으나, 리소스가 부족하면 배치
  
  + NoExecute: 톨러레이션에 해당 레이블이 없는 파드는 스케줄링 할 수 없고, 기존 파드도 설정을 무시 할 수 없다.
  
+ `Key=Value:Effect`의 의미는 톨러레이션에 의해 허용될 레이블이며, 해당 레이블이 없으면 효과에 의해 스케줄링하지 않는다는 의미


+ **테인트 설정**

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_Taint_get.png" alt="drawing" width="500"/>

+ `kubectl taint node kube-node3 env=production:NoSchedule` 로 설정한다.

+ `kubectl describe no | grep Taint` 로 설정이 잘되었는지 확인

#### 톨러레이션이 없는 레플리카셋
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_notoleration_yaml.png" alt="drawing" width="500"/>

#### 톨러레이션을 사용한 리소스

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_toleration_yaml.png" alt="drawing" width="500"/>


## 커든 및 드레인

+ 커든은 특정 노드에 파드가 스케줄링되지 않도록 하는 기능이다.

+ 테인트는 특정 노드를 특정 역할로 사용하기 위해 톨러레이션과 함께 사용하지만, 커든은 모든 파드의 스케줄링이 되지 않도록 한다.

+ 현재 배치되어 동작중인 파드에는 영향을 미치지 않는다. 새로 스케줄링되지 않도록만 하는것

+ **드레인**

+ 드레인은 관리적인 여러 이유, 유지보수의 목적으로 해당노드에 파드가 없어져야하는 경우, 모든 파드를 퇴고되고 다른노드로 이전한다.

+ 드레인을 설정하면 모든 파드를 이전하기 전 커든이 먼저 적용된다.

### 커든

+ **커든 명령**

+ `kubectl cordon 노드명` 으로 해당 노드를 커든시킬 수 있다.

+ `kubectl uncordon 노드명` 으로 커든이 적용되어있는 노드를 해제 할 수 있다.

### 드레인
+ ** 드레인 명령**

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_Drain_Warning.png" alt="drawing" width="500"/>

+ 지금 해당하는 파드들때문에 `Drain`이 작동하지 않는다는 문구다.

+ `kubectl drain kube-node1 --delete-local-data --ignore-daemonsets` 으로 강제실행 할 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_Drain.png" alt="drawing" width="500"/>

+ `Drain`을 강제실행 한 상태이고 `evirt`는 실행되고있는 파드들을 내보내고있다는 뜻

+ `Drain`이 완료되고 `kubectl get no`를 하게되면 해당노드는 `cordon`이 적용되어있다.

+ `Drain`에는 `cordon`이 포함되어있어서 드레인이 끝난후에는 커든이 되어있으니 `kubectl uncordon 노드명`으로 해제해줘야 정상적으로 스케줄링이 가능하다.
