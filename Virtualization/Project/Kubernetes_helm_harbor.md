# 쿠버네티스 Helm차트로 Harbor구성하기
## Helm 이란?
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/helm_logo.png" alt="drawing" width="400"/>

 한번의 커맨드 입력으로 클러스터 내에 리소스들을 설치 및 변경 할 수 있다.

`tar.gz` 확장자로 클러스터 리소스를 패키징하여 원격 저장소를 통해 공유 할 수 있다.


### Helm에 기본 구성

`Chart`는 Helm의 패키지의 포맷 `helm create <이름>`로 `Chart`에 구조를 생성 할 수 있다.

+ `Chart.yaml(yml)` : Chart의 정보를 정의하는 파일로 Chart의 이름 및 버전을 정의한다.

+ `Charts` : dependency chart 파일들이 디렉토리 아래에 생성된다.

+ `template` : k8s 리소스 템플릿이 보관되는 디렉토리이다.

  + `Notes.txt` : Chart를 설치 후 출력되는 내용을 정의한다.
  
  + `*.yaml` : 리소스 템플릿 파일형식
  
+ `values.yaml` : 템플릿에 사용될 변수들을 볼 수 있는 파일이다.

***

## Harbor란?

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/harbor_logo.png" alt="drawing" width="600"/>

## 실습 목차
1. Add Harbor Chart Repository

2. Make values.yaml
    PVC
    Domain
    Password
    ...

3. Create Namespace

4. Install Harbor Chart

5. Edit /etc/hosts with Client/All Nodes

6. Verify Harbor Portal

7. Add library(harbor) Chart Repository with Cert(ca.crt)

8. Allow Insecure Harbor Registry with All nodes
https://docs.docker.com/registry/insecure/
    1) /etc/docker/daemon.json
    2) /etc/docker/certs.d/<domain>/ca.crt

9. Create secret for Authentication of Harbor Registry 

출처: https://github.com/goharbor/harbor-helm
