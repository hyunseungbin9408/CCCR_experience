# Helm 패키지 관리자
## Helm 소개
+ 지금까지 리소스를 생성하기 위해 간단한 명령으로 가능했지만, 많은 yaml 오브젝트파일 생성하고 수정 관리

+ 웹 어플리케이션을 구성하기 위해서 많은 yaml 오브젝트 파일이 필요한데 이럴때 Helm은 관리의 복잡함을 Helm의 차트구성으로 구성, 배포, 관리를 쉽게 할 수 있다.

+ Helm Classic 프로젝트는 2015년 Kubecon에 소개되면서 알려지게 되었고, 2016년 1월 쿠버네티스 프로젝트와 통합

## Helm 설치

+ `wget https://get.helm.sh/helm-v3.1.2-linux-amd64.tar.gz` helm 바이너리를 다운

+ macOs 에서 설치 `brew install helm`

+ Ubuntu `sudo snap install helm --classic`

## Helm 기본 개념
+ `차트(chart)` = Helm패키지

+ `저장소(Repository) = Helm 차트가 저장된 저장소

+ `릴리즈(Release) = 파트가 클러스에 배포된 기본 단위
