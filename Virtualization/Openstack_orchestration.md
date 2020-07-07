# orchestration(heat) stack구성

## Generator로 web서버 stack만들기

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator.png" alt="drawing" width="700"/>

 + Generator에서 이러한 그래픽으로 스택에 필요한 리소스들을 하나씩 구성 할 수 있다.
 
 + 미리 전에 기본적으로 설치해둔 구성품들을 사용 할 수 있고 필요할때마다 리소스를 저 안으로 끌어다가 사용가능
 
 + 리소스들이 서로서로 연결되기 때문에 큰 범위에 리소스들을 먼저 설치하고 하위 리소스들을 설치하는게 좋다(개인적인생각).
 
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_server.png" alt="drawing" width="550"/>

```

  제일 먼저 구성한 리소스는 서버이다.
  
  서버구성에 필요한 정보들은 flavor과 부트를 어떠한 방식으로 할지이다.
  
  새로운 네트워크를 설치하고 연결할 예정이니 다른것은 건들필요없다.

```
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_network.png" alt="drawing" width="550"/>

```

  그 다음으로 구성한것이 네트워크이다.
  
  네트워크자체에서는 건들것이없고 이 네트워크 리소스가 있어야만
  
  서브넷과 포트가 작동하기 때문에 필수적으로 만들어 줘야한다.
  
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_subnet.png" alt="drawing" width="550"/>

```
  
  서브넷 설치단계이다.
  
  먼저 서브넷리소스를 끌어다가 구성하고 네트워크와 연결시켜주면
  
  서브넷안에 네트워크가 자동으로 변수로 들어간다.
  
  그 후에 ipv4로 구성하고 CIDR는 우리가 사용할 대역폭을 설정하면 끝이다.
  
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_port.png" alt="drawing" width="550"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_port2.png" alt="drawing" width="550"/>

```

  포트를 설치하는데 서브넷과 네트워크에 연결해주어야한다.
  
  보안그룹은 포트에서 설정해준다. 하지만 서버에도 보안그룹을 설정하면 스택설치가 불가능하니 참고하자.
  
  주소목록에 가면 아이피를 정할 수 있는데 DHCP를 사용할 예정이라 따로 건들지않고서 서브넷과 연결하여
  변수처리해야한다.
  
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_floatingIP.png" alt="drawing" width="550"/>

```

  외부망과 연결할 수 있도록 유동아이피를 설정하는데
  
  외부망은 미리 만들어두었고 Public으로 이름지었다.
  
  유동아이피는 포트와 연결해주면 된다.
  
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_routerinterface.png" alt="drawing" width="550"/>

```

  외부망과 내부망이 통신하려면 라우터가 필수적으로 필요하기때문에
  
  외부망을 설치할때 만들었던 라우터와 연결하기 위해서 인터페이스를 설정해줘야한다.
  
  라우터 인터페이스는 서브넷과 연결과 해주고 서브넷은 변수로 처리한다.
  
```
  
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_templeate.png" alt="drawing" width="550"/>

```
 
 기본적인 웹과 소통할 수 있는 서버구성이 완료되었고 스택을 만들기위해서 진행하기전에 처음이라면 오류많이 발생하기때문에 저장을 하고 진행 하는 것이 좋다.
 
 이런식으로 템플릿이 나온다. 우리가 리소스들을 그래픽으로 끌어와서 구성했지만
 
 이러한 형식으로도 구성할 수 있다.
 
 파일형식으로 다운받을 수 있고 바로 진행 할 수 있다.
 
 나는 바로 진행하였다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_templeate2.png" alt="drawing" width="550"/>

```

 진행하면 이러한 형식을 볼 수 있는데 하나라도 문제가 생기면 진행되지않기때문에
 
 어떠한 오류가 생기면 오류로그를 잘 보고 해결해야한다.

 파일형식으로도 만들수 있다.
 
```

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_stack.png" alt="drawing" width="550"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/openstack_heat_generator_instances.png" alt="drawing" width="550"/>

```

 스택을 구성하는데 문제가 없다면 이렇게 스택과 인스턴스가 같이 설치가 된다.
 
 웹서버 두개가 구성되었으니 이제 로드밸런서를 만들려고한다.
 
```
