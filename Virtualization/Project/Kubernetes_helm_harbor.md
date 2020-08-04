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

`Harbor`는 컨텐츠를 저장, 서명 및 스캔하는 오픈소스이고 클라우드 기본 레지스트리 프로젝트이다.0

`Harbor`는 보안, ID 및 관리와 같은 사용자가 일반적으로 필요로 하는 기능을 추가함

`Harbor`는 `CNCF(Cloud Native Computing Foundation)`에서 호스팅하고 있다.

### Harbor에 주요 기능

`클라우드 네이티브 레지스트리`: 컨테이너 이미지와 Helm차트 모두 지원하는 Harbor는 컨테이너 런타임 및 오케스트레이션 플랫폼과 같은 클라우드 네이티브 환경의 레지스트 역할을 한다.

`역할 기반 액세스 제어` : 사용자 및 리포지토리는 프로젝트를 통해 구성되고 사용자는 프로젝트에서 이미지 또는 Helm 차트에 대해 서로 다른 권한을 가질 수 있다.

` 정책 기반 복제` : 여러 필터가 있는 정책을 기반으로 여러 레지스트리 인스턴스 간에 이미지 및 차트를 복제 할 수 있다.
Harbor는 오류가 발생하면 자동으로 복제를 재시도 한다. 로드밸런싱, 고가용성(HA), 다중 데이터 센터, 하이브리드 및 다중 클라우드 시나리오에 적합하다.

`취약점 검색`: Harbor는 이미지를 정기적으로 스캔하여 사용자에게 취약점을 경고한다.

`LDAP/AD 지원` : Harbor는 사용자 인증 및 관리를 위해 기존 엔터프라이즈 LDAP/AD와 통합되며 LDAP 그룹을 Harbor로 가져오고 적절한 프로젝트 역할을 할당 할 수 있음

`OIDC 지원` : Harbor는 OIDC(OpenID Connect)를 활용하여 외부 인증 서버 또는 자격 증명 공급자가 인증 한 사용자의 자격 증명을 확인한다.

`쉬운 배포` : 온라인 및 오프라인 설치 관리자를 모두 제공한다. 또한 Helm Chart를 사용하여 Kubernetes에 Harbor를 배포 할 수 있음

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

출처: https://github.com/goharㅑ7
ㅐㅑㅐ 
ㅑㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅐㅗr/harbor-helm

