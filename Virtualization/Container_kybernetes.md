# 컨테이너
 ## 마이크로서비스 및 Devops
 ### 모놀리식 아키텍처
 + 단일 프로세스에서 실행되거나 몇몇 시스템에서 몇개의 프로세스로 실행되는 거대한 모놀리식 애플리케이션
 
 + 모놀리식 아키텍처에서는 애플리케이션을 매번 릴리스 할때마다 개발자가 전체 애플리케이션을 java의 경우 War파일로 패키징 하거나, Ruby on Rails또는 Node.js의 경우 단일 디렉토리 계층으로 묶어서 배포
 
 + **모놀리식 아키텍처의 장점**
 + 간단한 개발
 
 + 간편한 배포
 
 + 단순한 확장성
 
 + **모놀리식 아키텍처의 단점**
 
 + 코드 품질이 낮아짐 : 큰 APP을 처음 접하는 개발자는 APP을 이해하고 수정하는데 어렵고, 개발 및 업데이트속도가 느려질 수 있음
 
 + 애플리케이션의 시작이 오래걸림 : 규모가 큰 APP일 수록 런타임에서 APP시작이 오래 걸린다.
 
 + 애플리케이션의 지속적인 배포가 어려움 : 하나의 컴포넌트를 업데이트하기 위해 전체 APP을 다시 재배포해야하며, 모든 APP을 중단하고 다시 시작해야한다.
 
 + 애플리케이션 확장의 어려움 : 모놀리식 아키텍처에서는 각 컴포넌트별로 독립적으로 확장 할 수 없다. 이는 전체 APP을 확장해야하며, 이에 따라 시스템 및 하드웨어 자원소모가 많이 되고 클라우드의 경우에는 쓸데없는 리소스가 낭비되어 비용이 많이 나올 수 있음
 
 + 컴포넌트별 개발의 어려움: 애플리케이션 크기가 커지면 조직을 특정기능 한정으로 초점을 맞춘 팀으로 나눌 수 있다. 그러나 모놀리식 APP은 팀이 독립적으로 개발 및 업데이트를 못하게 한다.
 
 + 다양한 기술적용의 어려움 : 예를 들어 JAVA로 개발된 모놀리식 APP이 있다면, 일부 개발에 따라 다른 특정 버전을 사용해야 하는 경우나, 새로운 기술을 도입하기 위해 다른 언어로 개발해야하는 APP이 있는 경우 모놀리식 아키텍처로 개발된 아키텍처에서는 불가능하다.
   
 ### 마이크로서비스 아키텍처
 + 모놀리식 차키텍처가 크기가 커짐에 따라 발생한 문제점을 극복하기 위해 마이크로서비스라는 기능적이고 세분화되고 독립적으로 작동하는 방식을 사용
 
 + 마이크로서비스기반의 APP은 API를 통해 서로 다른 서비스와 통신
 
 + 마이크로서비스 사이에는 일반적인 동기방식인 HTTP/RESTful API 또는 비동기 방식인 AMQP프로토콜을 사용하여 통신한다.
 
 + 마이크로서비스는 각 기능을 구현하기 가장 적합한 언어로 개발 할 수 있다.
 
 + **마이크로서비스 아키텍처의 장점**
 
 + 크고 복잡한 애플리케이션을 지속적으로 배포 할 수 있음
 
   + 향상된 유지 보수성 : 각 서비스는 작기 때문에 이해하고 변경하기 쉬움
   
   + 테스트 용이성 : 각 서비스는 독립적으로 테스트 가능
   
   + 배포 효율성 : 각 서비스는 독립적으로 배포가능
   
   + 독립적으로 개발, 테스트, 배포 및 확장
   
 + 개발에 생산성이 높고 배포 속도가 높음
 
 + 향상된 장애 격리: 장애가 발생한 서비스만 영향을 받음
 
 + 다양한 기술 적용가능
 
 + **마이크로서비스 아키텍처의 단점**
 + 분산시스템 설계에 따른 복잡성
   + 서비스 간 통신 메커니즘을 따로 구현
   
   + 서비스 간 상호작용 테스트
   
 + 배포 및 관리 운영상의 복잡성
 
 + 증가된 리소스 소비
 
 ### DevOps
 + 애플리케이션을 개발하고 운영하는 경우, 개발 팀과 운영 팀 사이에서 가장 큰 문제는 개발 팀에서 APP을 개발하는 환경과 운영 팀에서 개발 된 APP을 프로덕션 시스템에 배포해 운영하는 환경과의 차이 때문에 문제가 발생
 
 + 이러한 차이는 개발자가 사용하는 하드웨어, 운영체제, 사용하는 라이브러리 및 버전까지 많은 부분에서 차이가 발생
 
 + 프로덕션 시스템은 보안패치나 최신 상태로 유지함으로 시간에 따른 변화가 발생
 
 + 이러한 차이점 및 변경사항으로 인해 일관된 환경을 제공하는것이 어려 울 수 있다.
 
 + 애플리케이션의 전체 라이프사이클을 함께 관리하는것이 효율적이라는것을 알게됨
 
 + 이런 소프트웨어 개발, 품질, 운영 팀의 소통 협업 및 통합을 강조하는 개발 환경 및 문화를 DevOps라고 한다.
 
 + 이러한 마이크로서비스 및 DevOps를 가능하게 하는 기술이 쿠버네티스
 
 + 쿠버네티스는 컨테이너 기술을 이용하여 표준화 되고 일관성 있는 환경을 제공하고 DevOps 문화를 가능하게함
 
 ## 컨테이너란?
  + 단일 컨트롤 호스트상에서 여러개의 고립된 리눅스 시스템들을 실행하기 위한 운영 시스템 레벨 가상화 방법
  
  + 애플리케이션을 실제 구동 환경으로부터 추상화할 수 있는 논리 패키징 메커니즘을 제공
  
  + 사설 데이터 센터나 퍼블릭 클라우드, 개발자의 개인 노트북 컴퓨터처럼 어떤 환경으로든 컨테이너 기반 애플리케이션을 쉽게 지속적으로 배포할 수 있음
  
  + 사용하는 회사들이 업무 영역을 깔끔하게 분리하여 관리 할 수 있다
  
  + 가상 머신과 마찬가지로 애플리케이션을 관련 라이브러리 및 종속 항목과 함께 패키지로 묶어 소프트웨어 서비스 구동을 위한 격리 환경을 마련
 
  + 어플리케이션을 실행하기 위해서 만듬
  
  + 하나의 컨테이너는 하나의 어플리케이션만 실행하는 것이 원칙
  
 
 ## 왜 컨테이너를 사용해야 하는가?
  + 운영체제 수준에서 가상화를 실시하여 다수의 컨테이너를 OS 커널에서 직접 구동한다.
  
  + **컨테이너는 훨씬 가볍고 운영체제 커널을 공유하며, 시작이 훨씬 빠르고 운영체제 전체 부팅보다 메모리를 훨씬 적게 차지한다**.
  
  + 컨테이너를 이용하여 개발자들은 분리되고 예측가능한 개발환경을 생성가능
  
  + 컨테이너는 애플리케이션에 필요한 소프트웨어 종속 항목도 포함할 수 있다. 개발자의 관점에서 이 모든 요소는 애플리케이션이 배포되는 최종 위치에 관계없이 항상 일관성이 있다.
  
  + 개발자와 IT 운영팀이 버그를 잡고 환경 차이를 진단하던 시간을 줄이고 사용자에게 신규 기능을 제공하는 데 집중할 수 있음
  
  + 컨테이너는 폭넓은 구동환경(Linux, Windows, Mac, 가상 머신, 베어메탈, 개발자의 컴퓨터, 데이터 센터, 온프레미스 환경, 퍼블릭 클라우드)을 가지기 때문에 개발 및 배포가 쉬워진다. 
  
  + vm으로 app을 배포하려면 vm마다 운영체제를 설치해줘야하기때문에 스토리지용량이 많이 소비가 되어서 비효율적이고 시간도 오래걸린다. 하지만 컨테이너는 하나의 어플리케이션만을 담당하기때문에 효율적이다.
  
 ## 컨테이너의 단점
  + 하나의 운영체제에 수평적으로 확장하기 때문에 운영체제가 문제가 발생하면 모든 컨테이너가 영향을 받는다.
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container.png" alt="drawing" width="700"/>
 
  + **컨테이너 실행 과정**
 
 
 ## 컨테이너를 설정할때 주의점
  + 컨테이너를 만들때 cpu제한과 메모리제한 무조건적으로 넣어준다.
  + cpu와 메모리에 가중치를 정해서 중요한 컨테이너순서대로 정해준다.
  + 어플리케이션 성격을 잘 이해해야한다.
    + 일시적인어플리케이션  (ls,hello world...)
    + 계속해서 실행되어야하는 어플리케이션 (httpd,mysql...)
  + 컨테이너와 레지스트리는 반드시 연결되어있어야 컨테이너가 이미지파일을 통해서 만들어진다.
 
 ### Cgroup
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_container_Cgourp.png" alt="drawing" width="700"/>

  + 프로세스 또는 스레드를 그룹화 하여 관리하는 기능
  + 컨테이너가 사용하는 리소스의 양을 제한 할 수 있다.
  + 같은 호스트에서 동작하는 서로 다른 컨테이너에 영향을 주지 않도록 막아주는 역할
  + 다음과 같은 리소스들을 제어할 수 있다.
    + 메모리
    + cpu
    + I/O
    + 네트워크
    + Device노드 (/dev/)
  
 ### namespace
  + VM에서는 각 머신별로 독립적인 공간을 제공하고 서로 충돌하지않는 기능을하는 namespaces을 리눅스에서는 커널에 내장함
  + 다수의 오브젝트를 격리 할 수 있다.
  + 동일한 호스트에서는 같은 PID를 가질 수 없지만 다른 namespace에서는 같은 PID를 가질 수 있다.
  + mnt: 호스트 파일시스템에 구애받지 않고 독립적으로 파일시스템을 마운트 가능
  + pid: 독립적인 프로세스 공간을 할당
  + net: namespace간에 network 충돌방지
  + ipc (systemV IPC): 독립적인 hostname할당
  + user: 독립적인 사용자 할당
  
  
 ### Layered FS (계층형 파일시스템)
  + 기본으로 **AUFS (Another union FS)** 사용했었음
  + 겹치는 파일을 계속해서 다운받을 필요없이 필요한 파일을 그때 마다 차이가 있는 파일만 불러오는 계층적 파일시스템
  + 컨테이너는 이러한 파일들을 읽고 쓸수있는 권한을 부여해줌
  + 코드가 안전하지않아서 레드햇에서 거부함으로써 이제는 더이상 포함되지않음 // Debian 에서는 사용함
  + 그래서 예전에는 LVM을 사용함 // Redhat 에서 사용
  + 지금은 Overlay2를 사용함 // 계층형 파일시스템
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_LayererdFS.png" alt="drawing" width="500"/>
  
***

## 쿠버네티스

### 쿠버네티스란?
+ 쿠버네티스란 명칭은 그리스어로 키잡이와 파일럿을 뜻한다.

+ 구글이 2014년도에 쿠버네티스 프로젝트를 오픈소스화했다.

+ 프로덕션 워크로드를 대규모로 운영하는 15년 이상의 경험과 커뮤니티의 최고의 아이디어와 적용 사례가 결합되어있다.

+ 클릭 한 번으로 작동하는 클러스터로 빠르게 시작

+ 멀티 영역과 리전 클러스터를 비롯한 고가용성의 제어 영역 활용

+ 자동 복구, 자동 업그레이드, 출시 채널을 통해 운영 오버헤드 제거

+ 컨테이너 이미지의 취약점 스캔, 데이터 암호화등의 기본 보안

+ 인프라, 애플리케이션, Kubernetes 관련 뷰를 이용한 통합 Clout Monitoring

### 왜 쿠버네티스를 사용하는가?
+ 컨테이너는 VM과 유사하지만 격리 속성을 완화하여 애플리케이션간에 운영체제를 공유함

+ Vm과 마찬가지로 컨테이너에는 자체 파일 시스템, CPU, 매모리, 프로세스공간이 있다.

+ 기본 인프라와 종속성을 끊었기 때문에 클라우드나 OS배포본에 모두 이식 할 수 있다.

+ 리소스 격리

+ 고효율 고집적인 자원 사용량

+ 서비스 디스커버리와 로드 밸런싱
  + 쿠버네티스는 DNS 이름을 사용하거나 자체 IP주소를 사용하여 컨테이너를 노출 할 수 있다.
  + 컨테이너에 대한 트래픽이 많으면, 쿠버네티스는 네트워크 트래픽을 로드밸런싱 하고 배포하여 배포가 안정적으로 이루어짐

+ 스토리지 오케스트레이션
  + 쿠버네티스를 사용하면 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소 시스템을 자동으로 탑재

+ 자동화된 빈 패킹
  + 배포된 컨테이너의 원하는 상태를 서술 할 수 있음
  + 현재 상태를 원하는 상태로 설정한 속도에 따라 변경 할 수 있음
  + 쿠버네티스를 자동화해서 배포용 새 컨테이너를 만들고, 기존 컨테이너를 제거하고 모든 리소스를 가장 잘 사용 할 수 있도록 해줌

+ 자동화된 복구
  + 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체하며, 사용자 정의 상태검사에 응하지않는 컨테이너를 죽이고 서비스 준비가 끝날때까지 그러한 과정을 클라이언트에 보여주지 않는다.
  
+ 시크릿과 구성관리
  + 암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리 할 수 있다.
  + 컨테이너 이미지를 재구성하지않고 스택 구성에 시크릿을 노출하지 않고도 시크릿 및 앱 구성을 배포 및 업데이트 
  
+ **Paas의 일부 기능만 제공한다.**

+ CI/CD (Continuos Integration/Continuous Delivery) 파이프라인
  + CI는 컴파일하고 빌드하는 과정
  + 지속적 통합, 지속적 배포를 제공하지 않음
  + 소스코드 배포 및 애플리케이션을 비드하지 않음

+ 애플리케이션 레벨의 서비스
  + 미들웨어, 빅 데이터, 데이터베이스, 캐시, 클러스터 스토리지 등 애플리케이션 레벨의 서비스는 제공하지 않음
 
+ 로깅, 모니터링, 경고 솔루션
  + 개념 증명(PoC)을 위한 통합, 메트릭 수집 및 노출 메커니즘은 제공
  + 그러나 쿠버네티스는 필요한 경우 PaaS로 제공되어야하는 여러 기능을 선택 적으로 쿠버네티스 위에 구성 할 수 있다.
  
### 쿠버네티스를 사용 할 수 있는 환경
+ chroot
+ Docker
+ LCX
+ Solaris Containers(Zones)
+ FreeBSD jail
+ WPARS(AIX)
+ rkt

### 쿠버네티스에 아키텍처 및 Hub and spoke

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_Hubandspoke.png" alt="drawing" width="700"/>

+ 쿠버네티스는 마스터에 kube-api-server를 통해서 모든게 이루어진다.

+ 그런것을 Hub and spoke라고 한다.

+ kubectl 이 이러한 진행도를 보인다.

+ controller는 Workload 라고 하고 Workload는 컨테이너이다.

+ **etcd : key value storage라고 하고 모든 정보는 이 스토리지에 저장된다.**

+ **kubernetes Controller Manager : 쿠버네티스에 컴포넌트들을 제어 담당**

+ **Cloud-Controller Manager : 클라우드를 제어 담당**

+ **Kube-scheduler : controller,workload에 스케줄을 담당**

+ **Nodes**

+ **kubelet**
  + wokerload가 마스터 server api와 통신하기 위한 에이전트 containerD로 runtime
  + 각 노드에서 실행되고 마스터로부터 제공받은 파드의 구성 정보를 받아서 컨테이너가 확실하게 동작하는 것을 관리하고 보장한다.
  
+ **kube-proxy**
  + wokerlaod에 네트워킹 포트포워딩을 하기 위한 필수 요소
  + 호스트 레벨의 네트워크 규칙을 구성하고 외부 연결을 파드에 대한 포워딩을 담당
  + 쿠버네티스의 서비스 추상화가 가능하도록 한다.
  
+ **Container Runtime : 컨테이너의 동작을 책임지는 구성요소, 지원하는 컨테이너 런타임은 다음과 같다**
  + Docker
  
  + Containerd 
  
  + Cri-o
  
  + rktlet
  
  + Kubernetes CRI를 구현한 모든 런타임

+ **CRI (Container Runtime Interface) : kubelet과 container runtime(어떠한 runtime을 사용함에따라 변함)사이에서 Kublet이 변하지않고 통신할수 있도록 해줌**

*** 

### 애드온
+ **쿠버네티스 클러스터에 추가 할 수 있는 확장 기능을 제공한다. 주요 에드온 구성요소는 다음과 같다.**

+ **클러스터 DNS** 
  + 쿠버네티스 클러스터 내에 여러 오브젝트에 대한 DNS 레코드를 제공하여 주소기반으로 오브젝트를 찾을 수 있다.
  
  + 클러스터 DNS 애드온은 추가 확장 기능에 포함되어 있지만 다른 애드온과 다르게 거의 필수 기능으로 사용된다.
  
+ **대시보드**
  + 쿠버네티스 클러스터를 위한 웹 기반의 인터페이스를 제공한다.
  
+ **컨테이너 리소스 모니터링**
  + 컨테이너들에 대한 리소스 사용량을 시계열 metric-server(실시간으로만 확인가능)를 사용하여 데이터를 저장하고 열람하기 위한 인터페이스를 제공
  
  + metric-server에서는 모니터링을 실시간으로만 가능하고 로그는 남지않음
  
  + 엔터프라이즈에서는 prometheus를 사용하는 것을 권장함
  
  + 그래서 중앙집권적 로그서버가 필요함
  
  + Elastic stack (Elasticsearch) 로 중앙집권적 로그서버를 구성예
  정
  
+ **클러스터 로깅**
  + 컨테이너 로그를 중앙 로그 저장소에 저장하고 관리하는 기능을 담당
 
***

### 쿠버네티스 API
+ 통신을 하기 위해서는 특정 api버전같아야하기 때문에 명시되어있어야함

#### 알파 버전 API
+ 버전 이름에 alpha가 포함된다. (v1alpha1)

+ 버그가 있을 수도 있으며, 이 기능을 활성화하면 버그가 노출 될 수 있다.

+ 기본적으로 비활성화 되어 있다.

+ 기능에 대한 기술 지원이 언제든 공지없이 중단 될 수 있다.

+ 다음 릴리즈 시 공지 없이 API의 호환성이 깨지는 방식으로 변경 될 수 있다.

+ 버그의 위험이 높고 장기간 지원되지 않으므로 단기간 테스트 용도의 클러스터만 사용

+ 개발자들만 사용함

#### 베타 버전 API
+ 버전 이름에 beta가 포함된다.

+ 코드가 잘 테스트 되었고, 이 기능을 활성화 해도 안전하다.

+ 기본적으로 활성화되어 있다.

+ 구체적인 내용이 변경 될 수 있지만, 전반적인 기능에 대한 기술 지원이 중단되지 않는다.

+ 오브젝트에 대한 스키마나 문법이 다음 베타 또는 안정화 릴리스에서 호환되지 않는 방식으로 바뀔 수는 있으나, 이전 할 수 있는 가이드를 제공

+ API 오브젝트의 삭제, 편집 또는 재생성이 필요 할 수도 있다. 이런 경우 애플리케이션의 다운타임이 필요 할 수 도 있다.

+ 다음 릴리즈에서 호환되지 않을 수도 있으므로 중요하지 않은 용도로만 사용하기를 권장한다.

#### 안정화 버전 API
+ 버전 이름이 vX 또는 X 정수이다.
+ 안정화 버전의 기능은 이후 여러 버전에 걸쳐서 소프트웨어 릴리스에 포함된다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_api-versions.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_api-resources.png" alt="drawing" width="500"/>

+ **제일 마지막 V1이 코어버전이다.**

+ api-resources들은 생성할 수 있는 리소스들이다.

+ 리소스들을 작업하기 위해서는 API그룹에 항상 속해있어야한다.

+ 그래서 이러한 명령어들로 확인해야한다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_api-resources_grep.png" alt="drawing" width="500"/>

+ 우리가 앞으로 리소스를 만들때 이런식으로 리소스들에 그룹을 확인하고 넣어주는 작업이 필요하다.

#### API그룹
+ API 그룹은 쿠버네티스에서 기능 추가 할때 해당 기능을 사용하기 위한 API를 더 쉽게 확장하도록 도와준다.
+ **코어그룹**
  + YAML: apiVersion: [VERSION]
  + HTTP REST: /api/[VERSION]
  
+ **코어이외의 그룹**
  + YAML: apiVersion: [GROUP]/[VERSION]
  + HTTP REST
  
***

### YAML 및 오브젝트 기본

#### YAML이란?

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_yaml_config.png" alt="drawing" width="500"/>

+ yaml,yml 파일을 만들때 기본적으로 적용할수있는 yaml에 필요한 들여쓰기등을 vi편집기에 적용시켰다.

#### YAML 요소
+ **스칼라/스트링**
```

banana
I am a boy
'I am a girl'

스칼라와 스트링은 하나의 문자열로 처리되지만 순서는 정해지지않는다.
```



+ **리스트/어레이**

```

- seoul
- Busan
- Incheon
-jeju(X)

대쉬 하나당 하나의 리스트라고 인식한다.

```

+ **해시/딕셔너리**
```

name: John Smith
age: 33
콜론을 이용하여 키: 값 형태로 한 줄에 하나의 요소를 표헌한다.

```

+ **해시의 리스트**

```

- name: John Smith
  age: 33
- name: Mary Smith
  age: 2
  
- name: Maria
age: 3 (X)
  리스트는 들여쓰기가 같아야 같은 리스트라고 인식한다.
  
 ```
 
 + **리스트의 해시**
 
 ```
 
 man:
   - John Smith
   - bill Jones
 women:
   - Mary Smith
   - Susan Williams
 
 ```
   
 #### YAML 문법
 + Yaml의 문자열은 UTF-8 또는 UTF-16의 유니코드 문자집합을 사용함
 
 + 공백 문자를 이용하여 들여쓰기로 계층구조를 구분함 (탭 문자는 들여쓰기에 사용하지 않음)
 
 + 하나의 스트림에 있는 여러 개의 YAML 문서를 구분하기 위해 시작은 하이픈 3개(---), 끝은 마침표 3개(...)를 사용함
 
 + 주석은 #으로 표시하며, 한 줄이 끝날 때까지 유요함
 
 + YAML 파일의 확장자는 yml 또는 yaml을 일반적으로 사용한다.
 
 
#### 쿠버네티스 오브젝트
+ 클러스터의 상태를 나타내기 위해 오브젝트 개체를 정의하여 사용함

+

##### 모든 오브젝트 정의 시 필수적으로 요구되는 필드

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_yaml_file.png" alt="drawing" width="400"/>

+ apiVerion: 오브젝트를 생성하기 위한 API버전 (V는 대문자)

+ kind: 오브젝트의 종류
  + 예: pod, services, replcaset, deployment 등
  
+ metadata: name, UID, namespace 등을 포함하는 기본적인 정보

+ spec: 오브젝트의 상태 정의
  + spec 내의 정의할 요소는 정의하고자 하는 오브젝트의 종류에 따라다르다.
 
 ##### 오브젝트 리소스 문서 확인 명령
 
 + **리소스를 구성할때 yaml파일에 들어가야하는 문법을 어떤식으로 정의하는지 나옴**
 
 + 기본적으로 리소스에 버전은 V1을 기본으로 나옴
 
 + 버전에 따라 같은리소스의 필드가 달라지니 만들기전에 필수적으로 확인해야함
 
 + kubectl explain 리소스
 
 + kubectl explain 리소스.spec
 
 + kubectl explain 리소스.spec.containers
 
 + kubectl explain 리소스.spec.containers.name
 
 + kubectl explain 리소스.spec.containers.image
 
 + kubectl explain 리소스.spec --recursive
 
***

### 오브젝트 관리
#### 명령형 명령어
+ kubectl 명령에 인수 또는 옵션을 사용하여 애플리케이션을 관리함
+ 일회성작업

+ 개발 환경에서 권장함

+ 가장 단순한 방법

```

kubectl run nginx --image nginx

kubectl create deployment nginx --image nginx

```

#### 명령형 오브젝트 구성
+ 오브젝트를 YAML 또는 JSON 형식으로 정의를 함
+ kubectl 명령은 YAML 또는 JSON 파일을 인수로 사용하여 오브젝트를 관리함
+ 오브젝트의 완전한 정의를 포함해야만 함

```

kubectl create -f nginx.yaml

kubectl delete -f nginx.yaml -f redis.yaml

kubectl replace -f nginx.yaml

```

#### 선언형 오브젝트 구성

+ 특정 디렉토리에 모든 오브젝트 파일을 배치함

+ kubectl 명령은 디렉토리를 인수로 사용하여 오브젝트를 관리함

```

kubectl diff -f configs\

kubectl apply -f configs\

kubectl diff -R -f configs\

kubectl apply -R -f configs

```
***
 
### 쿠버네티스 실습

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_help.png" alt="drawing" width="500"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_kubernetes_kubectl_help2.png" alt="drawing" width="500"/>

```

 쿠버네티스에 기본 실행명령어는 kubectl이고 --help를 통해서 다양한 명령어를 볼 수 있다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_status.png" alt="drawing" width="500"/>

```

kubectl cluster-info로 쿠버네티스가 클러스터에 api들이 작동하는것을 확인

nodes 들이 3개가 있는것을 확인

```
