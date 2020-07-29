# 쿠버네티스 스테이트풀셋
## 기존 컨트롤러의 문제점
+ 파드의 정보를 저장하려면 파드마다 저장소를 가져야한다. 하지만 컨트롤러로 만들어진 파드들은 같은 볼륨을 가진다.

+ 그다음은 여러 컨트롤러를 구성하고 컨트롤러마다 파드를 하나만 지정하는것인데 여러가지의 컨트롤러를 한꺼번에 관리하는것은 불가능

## 스테이트풀셋 소개

+ 레플리케이션 컨트롤러나 레플리카셋이 제공하는 파드는 각 별도의 볼륨을 사용 할 수 있는 방법을 제공하지않아서 하나의 볼륨을 사용할 수 밖에 없다.

+ 그래서 파드마다 각각의 볼륨을 갖기 위해서는 스테이트

### 가축과 애완동물
+ 스테이트풀셋은 파드가 문제가 생겨서 삭제되면 그전과 똑같은 상태에 파드를 생성할 수 있다.

+ 스테이트풀셋에서 생성하는 파드들은 이름을 정할 수 있다.

+ 스테이트풀셋에서 생성하는 파드는 순서가 정해져있다.

+ 스테이트풀셋과 헤드리스서비스를 같이 쓰면 파드에 FQDN이 정해져있어서 같은 서비스와 같은 파드를 정할 수 있다.

+ 순서에 맞게 파드들이 생성되기때문에 다른 컨트롤러보다 느리다.

+ 스테이트풀셋도 `updateStrategy`에서 롤링업데이트가 가능하다. 업데이트 스테이트풀셋은 마지막것부터 차례대로 생성된다.



### 스테이트풀셋 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Statefulset_yaml.png" alt="drawing" width="500"/>

+ 다른 컨트롤러와 비슷하지만 다른점은 `serviceName:`을 필수적으로 지정해야 한다는 것이다. 서비스를 지정할 수 있다.

+ 스테이트풀셋은 헤드리스 서비스와 같이 활성화시켜서 파드하나에 서비스를 접목시켜서 고정시킬 수 있다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Statefulset_volume.png" alt="drawing" width="500"/>

+ 스테이트풀셋은 `volumeClaimTemplates`으로 파드마다 각각 저장소를 정할 수 있고 생성된 파드를 삭제해도 저장소는 삭제되지않고 그대로 사용가능하다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Statefulset_get.png" alt="drawing" width="500"/>

+ 볼륨 서비스 파드가 하나처럼 묶여있다.
