# Helm 패키지 관리자
## Helm 소개
+ 지금까지 리소스를 생성하기 위해 간단한 명령으로 가능했지만, 많은 yaml 오브젝트파일 생성하고 수정 관리

+ 웹 어플리케이션을 구성하기 위해서 많은 yaml 오브젝트 파일이 필요한데 이럴때 Helm은 관리의 복잡함을 Helm의 차트구성으로 구성, 배포, 관리를 쉽게 할 수 있다.

+ Helm Classic 프로젝트는 2015년 Kubecon에 소개되면서 알려지게 되었고, 2016년 1월 쿠버네티스 프로젝트와 통합

## Helm 설치

+ `wget https://get.helm.sh/helm-v3.1.2-linux-amd64.tar.gz` helm 바이너리를 다운

+ `tar xf helm-v3.1.2-linux-amd64.tar.gz`

+ `sudo cp linux-amd64/helm /usr/bin or /usr/local/bin` helm 실행파일 적용

+ `helm version`으로 helm버전 확인

+ macOs 에서 설치 `brew install helm`

+ Ubuntu `sudo snap install helm --classic`

## Helm 기본 개념
+ `차트(chart)` = Helm패키지

+ `저장소(Repository) = Helm 차트가 저장된 저장소

+ `릴리즈(Release) = 파트가 클러스에 배포된 기본 단위

## Helm 차트 구조

+ Helm 차트는 쿠버네티스 리소스를 모아놓은 패키지, TAR Gzip으로 아카이브 및 압축
```
  mychart/
    chart.yaml
    value.yaml
    template/
```
+ helm 차트구조이다.

## Helm 차트 설치 및 관리

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Helm_install.png" alt="drawing" width="700"/>

+ `Helm install [NAME] [CHART] [FLAGS]`
  + `NAME` : 릴리즈 이름
  + `CHART`: 차트 이름
  + `FLAGS`: 옵션
  
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Helm_list.png" alt="drawing" width="700"/>

+ 다운받은 패키지 목록을 확인하는 `helm list` 명령어

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_Helm_uninstall.png" alt="drawing" width="700"/>

+ 다운받은 패키지를 삭제하는 `uninstall` 명령어

## Prometheus 모니터링
### 쿠버네티스 기본 모니터링 개요
+ 

