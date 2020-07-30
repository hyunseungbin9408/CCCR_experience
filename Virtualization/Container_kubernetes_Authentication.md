# 쿠버네티스 인증
## 인증 및 kubeconfig

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Anthentication.png" alt="drawing" width="600"/>

+ 모든 쿠버네티스 클러스터를 사용하는 사용자는 `kubectl`클라이언트나 `HTTP REST` 요청을 통해 API 서버에 접근한다.

+ 해당 사용자는 제공한 인증 정보를 바탕으로 API 접근 권한을 부여 받을 수 있다.

## 인증
### 사용자

+ 쿠버네티스 클러스터에는 쿠버네티스에서 관리하는 서비스계정과 일반 사용자가 있다.

+ `서비스 계정(Service Account)`은 쿠버네티스 API로 관리되는 쿠버네티스에 존재하는 사용자다.

+ `서비스 계정`은 시크릿에 자격증명 정보가 저장되어 있으며, API 요청시 해당 자격증명으로 인증을 수행하게 된다.

+ `일반 사용자`는 쿠버네티스 자체적으로 관리하지 않는, 쿠버네티스 클러스터 외부의, 외부 계정 관리 시스템과 연동되어 인증에 사용되는 사용자를 말한다.

+ API 서버에 요청할때 `서비스계정`이나 `일반 사용자`가 아닌 경우 `익명 사용자`로 처리된다.

### 인증 방법
+ **클라이언트 인증서**

  + X.509 기반의 TLS인증서
  
  + 클라이언트가 인증서와 키를 이용한 인증
  
  + 지금까지 모든 kubectl 명령에 사용했던 방식

+ **베어러 토큰**

  + HTTP 요청 헤어에 `Authorization: Bearer [TOKEN]` 토큰을 전송
  
  + 서비스 계정 토큰
  
  + `OAuth2 Bearer` 토큰

+ **인증 프록시**

  + HTTP 요청 헤어에 `X-Remote-User`등의 인증 정보 전송
  
+ 기본 HTTP 인증 (실무에서 절대 사용금지)
  
  + HTTP 요청 헤더에 `Authorization: Basic BASE64ENCODED(USER:PASSWORD) 인증 정보 전송
  
  + 간편한 인증으로 편의를 위해 만들어 놓음 (보안에 좋지못함)
  
  + 패스워드를 변경하기 위해 API 서버가 재시작 되어야 함
  
### kubeconfig 파일

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Anthentication_current_config.png" alt="drawing" width="500"/>

+ 지금 현재 쿠버네티스에서 사용하고있는 계정들이 정리되어있는 `config` 파일이다

### kubeconfig 파일 생성 및 관리

+ `mkidr config-practice` 연습용 디렉토리를 만든다.

+ `kubectl config --kubeconfig=config-test set-cluster production --server=https://1.2.3.4` 로 production 클러스터 생성

+ `kubectl config --kubeconfig=config-test set-cluster development --server=https://5.6.7.8` 같은 방법으로 development 클러스터 생성

+ `kubectl config --kubeconfig=config-test set-credentials admin --token=abc` admin사용자를 지정하고, admin사용자의 토큰을 지정

+ `kubectl config --kubeconfig=config-test set-credentials user --token=xyz` user사용자를 지정, user사용자의 토큰을 지정

+ `kubectl config --kubeconfig=config-test set-context prod-admin --cluster=production --namespace=default --user admin` 명령어로 production 클러스터, admin사용자, default 네임스페이스 정보를 묶어서 콘텍스트를 생성

+ `kubectl config --kubeconfig=config-test set-context prod-admin --cluster=development --namespace=devel --user user` 명령어로 development 클러스터, user사용자, devel 네임스페이스 정보를 묶어서 콘텍스트를 생성

+ `kubectl config --kubeconfig=config-test view` 로 config내용을 볼 수 있다

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Anthentication_current_config_view.png" alt="drawing" width="500"/>

### 클라이언트에서 작업하기

+ `.kube/config`

+ `curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.16.11/bin/linux/amd64/kubectl` 로 버전에 맞는 `kubectl`를 다운받는다.

+ `chmod +x kubectl` 로 실행권한을 준다.

+ `sudo mv kubectl /usr/local/bin`로 명령어를 실행 할 수있게 `/usr/bin/ 이나 /usr/local/bin/`에 넣어준다.

***

## 역할 기반 접근 제어
### 인증, 권한 
