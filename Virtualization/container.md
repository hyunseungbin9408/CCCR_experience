# 컨테이너

## 컨테이너란?
 ### Cgroup
 
 <img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Linux_container_Cgourp.png" alt="drawing" width="700"/>
 
  + 프로세스 또는 스레드를 그룹화 하여 관리하는 기능
  + 컨테이너가 사용하는 리소스의 양을 제한 할 수 있다.
  + 같은 호스트에서 동작하는 서로 다른 컨테이너에 영향을 주지 않도록 막아주는 역할
  
 ### namespace
  + 다수의 오브젝트를 격리 할 수 있다.
  + 동일한 호스트에서는 같은 PID를 가질 수 없지만 다른 namespace에서는 같은 PID를 가질 수 있다.
  
  
