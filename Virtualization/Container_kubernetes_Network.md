# 쿠버네티스 네트워크
## 클러스터 내부 서비스
+ 파드는 클러스터 외부의 요청이나 클러스터 내부의 다른 파드의 요청에 응답해야함

+ 파드가 다른 파드에서 제공하는 애플리케이션을 사용하기 위해서는 다른 파드를 찾을 수 있어야함

+ 쿠버네티스가 아닌 기존의 시스템은 애플리케이션이 동작하는 시스템의 호스트 이름이나 정적 IP를 할당하여 해당 애플리케이션을 찾을 수 있다.

+ 하지만 쿠버네티스 환경에서는 그렇게 할 수 없다.

+ **그러한 이유**
  + 파드는 일회성으로 동작하기 위해 설계되었고 언제든지 제거될수 있음
  
  + 특정 노드에 파드가 스케줄링 되고 IP주소가 동적으로 할당됨 클라이언트는 파드의 IP주소를 알 수 없다.
  
  + 분산 아키텍처 및 수평 스케일링의 경우 여러파드가 같은 애플리케이션을 제공한다. 각 파드마다 IP가 존재하고, 스케일링이 될 때마다 클라이언트가 해당 IP를 알 수 없다.
  
### 서비스 소개
+ 서비스는 쿠버네티스 시스템에서 같은 애플리케이션을 실행하고 있는 컨트롤러의 파드 그룹에 단일 네트워크 진입점을 제공하는 리소스

+ 서비스에 부여된 IP는 해당 서비스가 종료 될 때까지 변경되지않는다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_apiservice.png" alt="drawing" width="500"/>

+ 쿠버네티스에 기본적으로 설치되어있는 서비스이고 api(443/tcp)로 통신하기 위한 기본서비스이다.

### 서비스 생성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_service_create.png" alt="drwaing" width="500"/>

+ 서비스 리소스에는 API그룹이 따로없다.

+ 그래서 기본적인 v1으로 버전을 넣어준다.

+ spec에 app은 서비스가 향하는 `pod`로 적어준다.

+ 포트는 기본적으로 열어줄 포트와 접근할 포트(targetPort)를 적어준다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_service_ep.png" alt="drawing" width="500"/>

+ 기본 서비스에 값음 마스터노드IP와 API포트(6443)이 열려져있다.

+ 지금은 만든 서비스가 향하는 `pod`가 없어서 `none`이 되어있다.

### 파드 생성 및 엔드포인트 연결

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_service_epcheck.png" alt="drawing" width="500"/>

+ 파드를 생성하고 `label` 를 처음 서비스를 만들때 `selector`에 넣었던 `app`처럼 넣어준다.

+ `kubectl get ep`로 다시 서비스에 `endpoint`를 확인해보면 `endpoint`가 생긴 것을 알 수 있다.

### 서브시 접근 테스트

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_service_curl.png" alt="drawing" width="500"/>

+ 레플리카셋을 파드를 4개로 정해서 만들었고 `app= myapp-rs`로 서비스가 셀렉 할 수 있도록 통일시켜주었다.

+ 레플리카셋과 서비스를 생성하고 `endpoint`를 확인해보니 서비스에 컨트롤러로 생성한 파드들이 들어가있는것을 확인했다.

+ 그후에 `kubectl run nettool2 -it --image=c1t1d0s7/network-multitool --generator=run-pod/v1 --rm=true bash` 로 curl를 실행할수있는 app을 생성했다.

+ `--generator=run-pod/v1`는 파드만 생성 할 것이라는 명령어이고 이 `generator`가 없다면 `deployment` 

+ app을 생성할때 `--rm=true` 명령어를 넣어주면 `-it bash`로 접속한 후에 `exit`로 접속종료를 하면 종료와 함께 app이 삭제된다.


<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_service_curl_check.png" alt="drawing" width="500"/>

+ app안에서 서비스에 연결되어있는 파드들에 홈페이지에 접속을 하면 잘 연결되는것을 확인했다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_service_LoadBalancer.png" alt="drawing" width="500"/>

+ 이 서비스가 로드밸런스가 작동되는지도 확인했다.

### 서비스의 세션 어피니티 구성
+ 세션을 계속유지하고 싶지만 로드밸런스때문에 다른 웹으로 가는것을 막기위한 세션 어피니티이다.
+ 클라이언트를 같은 어플리케이션에 항상 접속 할 수 있도록 해주는것

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_ses_aff_service_create.png" alt="drawing" width="500"/>

+ 기본적인 서비스를 만드는것과 다르지않다.

+ `sessionAffinity`에 어떠한 ip를 고정시킬것인지 확인하는 곳에 `ClientIP`로 입력해주면 서비스로 ip를 접속했을때 같은 ip로 접속한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_ses_aff_service_ep.png" alt="drawing" width="500"/>

+ 서비스를 만들고 endpoint에 파드들이 들어가있는지 확인했다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_ses_aff_service_curl.png" alt="drawing" width="500"/>

+ 그리고 접속을 확인하는 파드를생성해서 서비스에 ip로 접속해도 분산시키지 않고 처음 접속했던 ip로 접속하는것을 알 수 있다.
