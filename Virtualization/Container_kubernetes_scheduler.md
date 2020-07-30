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

#### 노드 레이블 부여

#### 노드 어피니티 오브젝트

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Scheduler_affiniti_yaml.png" alt="drawing" width="500"/>

#### 노드 어피니티가 적용된 리소스 생성

### 파드 어피니티 및 안티 어피니티
+ 파드 어피니티 및 안티 어피니티는 파드간에 같은 노드에 배치 할것인지, 다른 노드에 배치할 것인지 선호도를 지정할 수 있다.
