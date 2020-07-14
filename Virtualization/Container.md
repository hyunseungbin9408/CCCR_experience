# 컨테이너
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
  +
  
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
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_overlay2.png" alt="drawing" width="500"/>
  
 ### 가상화와 컨테이너 비교
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Virtualization_VS_Container.png" alt="drawing" width="500"/>
 
 ### 도커 (DocKer)
   #### 도커(DocKer)란?
   + 2008년에 dotCloud를 통해 동명의 컨테이너 기술과 함께 Docker가 등장
   
   + 도커는 개발자와 시스템 관리자를 위한 오픈소스 플랫폼
   
   + 분산된 애플리케이션을 빌드하거나 배포, 실행 할 수 있다.
   
   + Docker inc.는 Docker 커뮤니티의 활동에 기반을 두고 있으며 Docker 커뮤니티의 보안을 강화하고 개선 사항을 공유하여 커뮤니티를 발전시키고 있다.
   
   #### 도커를 사용하는 이유는?
   + Docker를 사용하면 컨테이너를 매우 가벼운 모듈식 가상 머신처럼 다룰 수 있음
   
   + 컨테이너를 구축, 배포, 복사하고 한 환경에서 다른 환경으로 이동하는 등 유연하게 사용할 수 있음
   
   + 가상화를 위한 에뮬레이터 단계가 없어서 오버헤드가 적고 애플리케이션 컨테이너를 지원
   
   + LXC에서 지원하는 대부분의 리눅스 시스템에서 동작 할 수 있어서 환경에 크게 구애받지 않는다.
   
   + 다수의 에플리케이션을 동일한 인스턴트에서 실행 할 수 있기때문에 자원의 효율성을 높일 수 있다.
   
   #### 도커 버전
   + CE(Community Edition) -> 19.3 버전이 마지막
     + 오픈소스버전 --> 새로운 버전이 나오면 그 전 버전의 지원이 끊김
     + Stable (3M) --> 이젠 지원안함
     + Edge (1M) --> Nightly Build (매일 새벽 업데이트 빌드)
   + EE (Enterprise Edition) (3M)
     + 기업대상으로 서포트제공 (비용이 듬)
     
  ### 도커 스토리지
   + 기본적으로 컨테이너에 생성되는 모든 파일은 컨테이너 레이어에 저장
   + 이 데이터들은 컨테이너와 함께 삭제되는 런타임 데이터
   + 데이터를 영구적으로 저장하려면 반드시 볼륨을 사용
   
   #### Bind Mount
   + 초기 도커부터 사용했던 방식
   + 호스트의 특정 디렉토리와 컨테이너의 디렉토리를 연결하는 방식
   + 쉽게 사용할 수 있지만 도커에 의해 관리되지 않기때문에 따로 기록하지않으면 관리가 힘듬
   + 성능이 뛰어나지만 호스트의 파일 시스템에 대한 의존도가 높음
   + 단점
   + 호스트의 민감한 파일까지 접근 할 수 있음으로 보안 측면에 문제가 발생 할 수 있음
   + **실습**
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_volume_bindmount_run.png" alt="drawing" width="500"/>
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_volume_bindmount_inspect.png" alt="drawing" width="500"/>
 
   + 컨테이너에 설정파일전용으로 많이 사용
   + /test:ro 읽기전용으로도 사용가능
   + 호스트의 파일또는 디렉토리 구조가 컨테이너의 Bind Mount와 일치하도록 보장하는경우
   
   #### 볼륨
   + 도커에 의해 관리되는 스토리지
   + docker명령어로 생성 할 수 있음, 사용하지 않은 볼륨도 삭제가능
   + **docker volume prune 으로 사용하지않은 볼륨만 삭제가능**
   + 컨테이너가 라이프사이클이 짧기때문에 볼륨은 분리하여 사용하는게 효율적이다.
   + 컨테이너가 생성한 파일들을 저장하는 용도로 사용함
   
   <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_volume_create_run.png" alt="drawing" width="500"/>
   
   <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_volume_mysql.png" alt="drawing" width="500"/>
   
  ``` 
  
   원래는 vol1이라는것을 생성하지않았고 vol2만 생성한 상태에서 데이터베이스 컨테이너를 만들때 vol1을 선언해봤더니 vol1이 생성되었다.
   vol2로 새로운 데이터베이스 컨테이너를 생성했고 mysql를 만들때 필요한 환경변수를 선언하고 다시 데이터베이스를 삭제한 후에
   다시 같은 볼륨으로 새로운 데이터베이스를 설치할때에는 환경변수를 선언하지않더라도 설치가 가능하다.
   vol2에 사용자 정보가 들어가있기 때문이다.
   이래서 볼륨을 따로 독립적으로 존재하는것이 시간과 정보둘다 보존 할 수 있는 좋은 방법
 
 ```
 
 ### 도커 네트워크
  + 컨테이너 네트워크는 호스트의 네트워크를 그대로 받는다.
  + 호스트에 80번 포트가 열려있으면 httpd 컨테이너를 만들 수 없다.
  + 네트워크 종류에 따라 다른 역할을 하는 컨테이너를 만들수있다.
    + 내부통신만 할 수 있는 host를 넣고 데이터베이스를 만들거나
    + 통신자체가 안되는 (none)을 사용해서 데이터백업이나 데이터가공 서버를 만든다.
    
    
 ### 도커파일
  + Entrypoint 는 쉘스크립트나 실행파일들이 들어간다.
  + CMD는 아규먼트나 command들이 들어간다.
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_file_Entrypoint_cmd.png" alt="drawing" width="500"/>

  + ENTRYPOINT는 항상먼저 실행되고 컨테이너의 실행파일이나 영향이 강한 명령어가 들어감
  + CMD는 항상 ENTRYPOINT 명령어 뒤에 붙는다.
  + CMD는 아규먼트나 변수같은 변하는 명령어를 넣는다.
  
  ```
  RUN, CMD, ENTRYPOINT
  
  CMD "/usr/sbin/httpd -D FOREGROUND" <-- shell // 파일이 있어야만 실행가능
  
  CMD ["httpd", "-D", "FOREGROUND"] <-- exec // 그대로 실행가능 JSON배열 방식 손상없이 입력가능
  
  CMD ["sh","-c","httpd","-D","FOREGROUND"] // exec방식으로 쉘 실행
  
  ```
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_file_exec_sh.png"
  alt="drawing" width="500"/>
  
  + bash위에서 명령어를 실행하면 기본값으로 bash가 들어가서 그 위에 덮어씌어짐
  + exec는 bash를 넣지않는다면 bash
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_dockerfile.png" alt="drawing" width="500"/>
  
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_dockerfile_build.png" alt="drawing"
  width="500"/>
  
  + docker build -t web:v1 . 을 입력하면 지금 호스트에 있는 파일로 빌드를 할때 적용한다는 뜻
  + 빌드를 할때 Dokerfile에 의해서 만들어진다.
  + 이미지에 layer를 담당하는 명령어는 RUN,ADD,COPY이다.
  + 이미지는 FROM Centos 를 가져온다는 뜻
  + RUN은 컨테이너에서 실행하는 명령어
  + ENV는 환경변수 선언
  + ADD는 호스트파일을 컨테이너에 넣는다는 명령어
  + VOLUME은 
 ***
     
 ### 도커 실습
  #### 도커 설치
  + 1) 사전패키지 설치
  
 ```
  
  sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
  
 ```
 
  + 2) yum 저장소 설정
  
```

 sudo yum-config-manager \
 --add-repo \
 https://download.docker.com/linux/centos/docker-ce.repo
 
 ```
 
 +  3) docker-ce 설치
 
 ```
  
  sudo yum install -y docker-ce docker-ce-cli containerd.io
  
  설치가 다되면
  
  sudo systemctl start docker
  sudo systemctl enable docker
  
 ``` 
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_status.png" alt="drawing" width="700"/>
 
 + 4) docker group add 및 도커 버전 확인
 
 ``` 
  설치 후에 바로 docker 를 쳐보면 권한이 없다고 뜬다.
  관리자가 아닌이상 권한이 없기때문에
  
  sudo usermod -aG docker 사용자
  
  Docker그룹에 사용자를 추가해주면 docker명령어를 사용 할 수 있다.
  
 ```
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_group.png" alt="drawing" width="700"/>
 
 ```
 
  hello run hello-world
  
  를 선언하면 다음과 같은 출력이 나온다.
  
  이미지파일이 없어서 도커허브에서 가져왔다는 말과
  
  허브에서 가져와서 실행한 출력문
  
  도커가 어떤식으로 컨테이너를 실행 했는지 순서가 출력됌
  
 ```
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_helloworld.png" alt="drawing" width="700"/>
 
  + **이미지파일을 생성할때 반드시 태그가 존재하고 선언하지 않으면 latest가 기본값으로 들어감**
  
  + **이미지파일에 태그가 직접선언 되어지지않고 latest로 되어있으면 함부로 사용해서는 안됌** // 어떠한 버전을 뜻하는지 모르기때문
  
  + 컨테이너는 반드시 이미지가 필요하고 없다면 Docker hub에서 가져옴
 
 ***
 ```
  도커 이미지파일을 docker image inspect hello-world를 실행하면
  
  이미지정보들이 나온다.
  
  config밑에 cmd를 보면 이 이미지를 실행하는 커맨드가 나온다.
  
 ```
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_helloworld_filecmd.png" alt="drawing" width="500"/>
  
 #### 도커 명령어
 
  + **도커 명령어에는 2개의 명령어와 3개의 명령어를 사용하는 방식이있다. 하지만 3개의 명령어로 사용하는것이 조금 더 명확하기 때문에 3개의 명령어를 사용하겠다.**
 
  + **Docker images : 현재 docker에 가지고있는 image list**
  
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_images.png" alt="drawing" width="500"/>
 
  +  **Docker pull : 이미지를 다운받을 때 사용하는 명령어**
  
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_pull.png" alt="drawing" width="500"/>

 + **Docker container ps - a : 지금까지 실행했던 컨테이너들**
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_container-ps.png" alt="drawing" width="500"/>
 
 + **Docker container run -it ubuntu bash : 이미지 파일을 터미널에서 bash로 실행**
   + bash를 굳이 쓸필요가 없고 기본적으로 실행되는 명령어와 다른 명령어를 실행할때 사용함 
   + 이런식으로 배포판으로 운영체제 이미지파일은 그자체로 사용하는것이 아님
   + 운영체제이미지파일들은 그 운영체제만의 고유한 라이브러리를 가지고있어서 계층적파일시스템을 이용해서 사용함
   ##### Attach 모드: -i -t
   
   <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_container-run.png" alt="drawing" width="500"/>
   
   + 실행중인 컨테이너에 접근하여 확인 할 수 있음
   + -i 는 입력을 받으려고 항상 대기하라 하고 명령하는 명령어
   + -t 는 터미널에 bash를 띄우라는 명령어
   + 컨테이너(어플리케이션)에 쉘이 없다면 bash를 실행 할 수 없다.
   + Attach는 실행하고있는 프로세스에 접속하는 것
   + create 
   
   ##### exec 모드 : 
   + docker container exec -it bash 컨테이너이름 
   + exec로 추가 명령어를 실행할때에는 컨테이너가 실행되어있어야한다.
   + exec로 -it로 접속하여 넣을때에는 반드시 처음에 만들었던 같은 쉘을 넣어야한다.
   + exec


 #### Docker run -e "ABC=123" centos
  <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_docker_run_env.png" alt="drawing" width="500"/>
  
  + 컨테이너를 만들때 컨테이너내에 환경변수를 넣어줄수있다.
  + mysql처럼 mysql에 접속할때 필요한 패스워드들을 넣어줄 수 있다. 넣지않으면 실행이 안됌 // 데이터베이스를 만들때 패스워드를 일정한 패스워드보다 랜덤으로 넣는게 좋다.
  
 #### Docker top : Process List
 
 #### Docker stats: HW Resource usage
 
 #### Docker attach: Exist STDIN,STDOUT
 
 #### Docker exec: Addtional Application(Process)
 
 #### Docker logs: container 로그들이 남음
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_container_logs.png" alt="drawing" width="500"/>
  + 컨테이너를 삭제하면 로그들도 같이 삭제
  
 #### Docker cp : 파일을 컨테이너로 복사
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_copy.png" alt="drawing" width="500"/>
 
 #### Docker diff : 파일의 상태를 출력
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_Container_diff.png" alt="drawing" width="500"/>
   + A: 파일이 추가
   + C: 파일이 변경
   + D: 파일이 삭제
   
   

