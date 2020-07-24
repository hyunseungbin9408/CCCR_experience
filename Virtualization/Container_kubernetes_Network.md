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

### 포트 이름 참조
#### 포트이름을 사용한 레플리카셋 및 서비스 생성
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_nport_create.png" alt="drawing" width="500"/>

+ yaml 파일로 서비스를 생성할때 포트의 이름을 정할 수있다.
+ 포트의 이름을 먼저 정하면 좋은것이 생성하기전에 rs에 포트들을 통합시킬수 있기때문에 편리하다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_nport_edit.png" alt="drawing" width="500"/>

+ 실행중인 파드들이 있는 레플리카셋에 파드포트 정보를 바꿀수있다.
+ 변경한 정보들은 실행중인 파드들에게는 적용이 안되고 다음번 생성되는 파드들에 적용이된다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetest_nport_ep.png" alt="drawing" width="500"/>

## 서비스 탐색
### 환경변수를 이용한 서비스 탐색

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_dns_rs_dns.png" alt="drawing" width="500"/>

+ 환경변수중 많은 부분이 kubernetes 서비스 및 myapp 서비스의 IP, 포트에 관한 변수와 값으로 구성되어 있음

+ 대표적으로 다음과 같은 환경 변수를 참조

  + MYNAPP_SVC_SERVICE_HOST=아이피
  
  + MYNAPP_SVC_SERVICE_PORT=아이피
  
  + MYNAPP_SVC_,KUBERNETES_SVC_ 이름은 실제 서비스의 이름과 매핑

### DNS를 이용한 서비스 탐색
+ 쿠버네티스 클러스터는 클러스터 시스템 내부에서 사용할 수 있는 DNS서버가 작동하고있다.

+ 이미 kube-system 네임스페이스에 DNS관련 파드 및 컨트롤러 서비스가 존재

#### DNS

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_dns_kube_system.png" alt="drawing" width="500"/>

+ `kube-system` 네이스페이스에 DNS관련 파드를 확인해보자. DNS 관련 파드는 k8s-app=kube-dns를 확인

+ DNS관련 서비스인 `service / coredns` 서비스가 있으며 10.233.0.3 IP로 접근 할 수 있다

+ 표준 DNS포트인 53으로 서비스하고 있음

#### 파드 내부 DNS 설정확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_dns_resolveconf.png" alt="drawing" width="500"/>

+ 지금 실행되고있는 파드에 `kubectl exec myrep-rs-nport-mlxxl -- cat /etc/resolv.conf` 로 DNS를 확인

+ 하지만 coredns 주소인 10.233.0.3가 아니라 169.254.25.10 으로 되어있다.

+ 그 이유는 모든 파드들에 DNS요청이 `10.233.0.3` 으로 몰리는것을 방지하기 위해서 노드마다 DNS Cache를 가지고있다.

+ 파드들에 요청을 한꺼번에 모아서 중앙 DNS로 가서 Cache를 들고오는 방식

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_dns_kube_system_ip.png" alt="drawing" width="500"/>

+ 이런식으로 데몬셋으로 DNS서버들이 구성되어있다는걸 알 수 있다.

+ 현재 우리 노드구성이 마스터 1대, 워커노드 3대 총 4대로 이루어져 있고 그 수에 맞춰서 cache가 생성되어있다.

#### FQDN을 이용한 서비스 탐색

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_dns_FQDN.png" alt="drawing" width="500"/>

+ `kubectl run nettool3 -it --image=c1t1d0s7/network-multitool --generator=run-pod/v1 --rm=true bash` 으로 `curl`접속을 도와줄 파드를 생성했다.

+ `curl http://myapp-svc-ses-aff`로 서비스 이름을 그대로 쓰면 DNScache를 거쳐서 접속이 된다.

+ 서비스이름뒤에 .`default` 을 입력하는것은 서비스 리소스의 네임스페이스 이름

+ .svc : 서비스 그 자체를 의미함

+ cluster.local: 쿠버네티스 클러스터 도메인

## 클러스터 외부 서비스
+ 쿠버네티스의 클러스터에서 웹의 프론트엔드 서비스를 실해하는 파드의 경우 쿠버네티스 클러스터의 외부로 노출시켜 접근 가능하도록 구성해야한다.

+ 서비스의 종류가 `ClusterIP`이다. 클러스터 내부 IP만 할당되어있고 클러스터 외부 Ip는 할당되어있지않다.

+ **서비스의 종류**

+ ClusterIP
  + 클러스터 내부용 서비스
  
+ NodePort
  + 쿠버네티스 모든노드에 외부 접근용 포트를 할당함
  
  + 노드의 포트를 사용하여 외부에서 접근가능
  
  + 노드의 포트로 접근하면 서비스에 의해 파드로 리다이렉션 함
  
  + 파드를 실행하고 있지 않는 노드에도 포트가 할당되고 접근 가능함
  
+ LoadBalancer
  + NodePort의 확장판
  
  + 클러스터 외부의 로드 밸런서를 사용하여 외부에서 접근 가능
  
  + 외부 로드 밸런서로 접근하면 서비스를 통해 파드로 리다이렉션 함
  
  + 클라우드 공급업체에서 지원하는 기능
  
+ ExternalName

  + 외부에서 접근하기 위한 종류가 아님
  
  + 외부의 특정 FQDN에 대한 CNAME 매핑을 제공
  
  + 파드가 CNAME을 이용해 특정 FQDN과 통신하기 위함
  
### 외부 서비스용 레플리카셋 생성 및 확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_enp_create.png" alt="drawing" width="500"/>

+ `type= NodePort`로 설정하고 노드에 포트번호는 30000~32767까지라 그사이로 설정해준다.

+ 다른 것은 서비스와 동일하다.

+ `kubectl get ep` 서비스에 파드들이 잘 적용되었는지 확인

+ 노드로 접근할 것이기때문에 `kubectl get nodes -o wide`로 노드들에 IP를 확인한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_enp_curl.png" alt="drawing" width="500"/>

+ `kubectl run nettool -it --image=c1t1d0s7/network-multitool --generator=run-pod/v1 --rm -- bash` 파드를 생성한다.

+ 노드들에 Ip와 서비스에 정했던 `NodePort`로 접근하면 통신이 잘 된다는걸 알 수 있다.
