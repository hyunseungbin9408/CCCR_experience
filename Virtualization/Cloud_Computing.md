# 클라우드 컴퓨팅 기술
## 하이퍼 바이저
 + 하드웨어를 소프트웨어 파티셔닝을 통해 가상머신에게 제공하는 소프웨어
 + 모니터링, 시스템 자원관리, 가상머신의 독립성 유지
 
 ### 하이퍼 바이저 종류
  #### 1) 네이티브 (Native/Bare-metal) 방식 하이퍼바이저
   <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/native%20or%20bare-metal%20virtualization_model.png" alt="drawing" width="250"/>
   
   + 호스트 운영체제가 없기 때문에 시스템 자원을 가상화에만 전부 사용가능 (Full Virtualzation)
   + **관리하는 엔진이 없다면 가상머신을 생성하거나 관리 할 수 없음**
   + 대표적인 제품은 VMM (Virtualization Machine Manager)이 있다.
   
  #### 2) 호스트 방식의 하이퍼바이저
   <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Host_Virtualization_model.png" alt="drawing" width="250"/>
   
   + 사용자가 이미사용하고 있는 운영체제위에 하이퍼바이저를 설치하는 방식
   + 간편하게 설치 할 수 있는 장점
   + 대표적인 제품으로는 Oracle의 VirtualBox 와 리눅스의 KVM이 있다.
   
