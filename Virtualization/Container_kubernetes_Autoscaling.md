# 쿠버네티스 오토스케일링
## 파드의 리소스 관리
+ 파드가 생성할때 리소스를 요청하면 요청한 만큼의 리소스가 있는 노드를 지정해준다.

## 리소스 요청
### 현재 리소스사용량 확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Autoscaling_top.png" alt="drawing" width="500"/>

+ `kubectl top nodes`로 쿠버네티스를 구성하는 노드들에 리소스 사용량을 알 수 있다.

+ `kubectl top po 파드명`으로 실행되고 있는 파드들에 리소스 사용량

### 파드 생성 리소스 제한

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Autoscaling_yaml.png" alt="drawing" width="500"/>

+ `yaml` 파일에 `request`는 파드에 최소리소스이다.

+ `limits`는 파드가 사용할수 있는 최대한 사용량

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Autoscaling_request.png" alt="drawing" width="500"/>

+ `request`를 지정하지않고 `limits`만 주는경우에는 파드에 `request`는 `limits`과 똑같이 된다.
