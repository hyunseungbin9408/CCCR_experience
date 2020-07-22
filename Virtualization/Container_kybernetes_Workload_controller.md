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
