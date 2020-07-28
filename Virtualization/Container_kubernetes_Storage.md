# 쿠버네티스 스토리지

## 볼륨
+ 컨테이너 내의 디스크에 있는 파일은 임시적이다.
+ 컨테이너에서 실행 될 때 애플리케이션에 적지않은 몇 가지 문제가 발생한다.
  + 첫째로 컨테이너가 충돌되면, kublet은 컨테이너를 재시작시키지만, 컨테이너는 깨끗한 상태로 시작되기 때문에 기존 파일이 유실된다.
  + 둘째로 pod에서 컨테이너를 함께 실행할때 컨테이너 사이에 파일을 공유해야 하는 경우가 자주 발생한다.
+ 쿠버네티스의 볼륨 추상화는 이 두가지 문제를 모두 해결한다.

### 배경
#### 도커볼륨
+ 도커는 다소 느슨하고, 덜 관리되지만 볼륨이라는 개념을 가지고 있다.
+ 도커에서 볼륨은 단순한 디스크 내 디렉터리 또는 다른 컨테이너에 있는 디렉터리다.
+ 수명은 관리되지 않으며 최근까지는 로컬 디스크 백업 볼륨만 있었다.
+ 도커는 이제 볼륨 드라이버를 제공하지만, 현재 기능은 매우 제한되어 있다.

#### 쿠버네티스 볼륨
+ 쿠버네티스 볼륨은 그것을 둘러싼 파드와 동일한 명시적인 수명을 가진다.
+ 그 결과로 볼륨은 파드 내에서 실행되는 모든 컨테이너보다 수명이 길고, 컨테이너를 다시 시작해도 데이터가 보존된다.
+ 물론 파드가 존재하지 않으면, 볼륨도 존재하지 않는다.
+ 이보다 더 중요한 것은 쿠버네티스가 많은 유형의 볼륨을 지원하고 파드는 여러 볼륨을 동시에 사용 할 수 있다.
+ 기본적으로 볼륨은 디렉터리일 뿐이며, 일부 데이터가 있을 수 있다.
+ 파드 내 컨테이너에서 접근 할 수 있다.
+ 디렉터리 생성방식, 이를 지원하는 매체와 내용은 사용된 특정볼륨의 유형에 따라 결정된다.
+ 볼륨을 사용하기 위해 파드는 파드에 제공할 볼륨과 컨테이너에 마운트할 위치를 지정한다.

### 볼륨 종류

+ empthDir
  + 임시로 데이터를 저장하는 빈 볼륨
  
+ gitRepo
  + 내부적으로 emptyDir 기능을 이용하여, 초기에 Git 리포지토리의 내용을 채워서 제공하는 볼륨, **더이상 사용되지 않는다.**

+ HostPath
  + 쿠버네팃 클러스터 노드의 파일시스템을 제공하는 볼륨
  
+ 네트워크 스토리지 볼륨
  + cephfs, cinder, fc, flexVolume, flocker, gluserfs, quobyte, iscsi, nfs, rbd, vsphereVolume, scaleIO 등
  
+ 클라우드 스토리지 볼륨
  + awsElasticBlockStore, azureDisk, azureFile, gcePersistentDisk
  
+ 정적/동적 프로비저닝 볼륨
  + persistentVolumeClaim
  
+ 특수유형 볼륨
  + configMap, secret

### EmptyDir 볼륨
#### emptyDir 볼륨 소개

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_sh_do.png" alt="drawing" width="500"/>

+ 쉘스크립트와 도커파일을 만들고 필드하는 과정

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_yaml.png" alt="drawing" width="500"/>

+ 기본 컨트롤러는 레플리카셋으로 구성하고 `volumeMounts` 와 `mountPath` 우리가 생성했던 포춘 스크립트 주소를 넣어주었다.

+ 밑에 볼륨이름과 컨테이너 볼륨이름을 똑같게해야 적용이된다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_cat.png" alt="drawing" width="500"/>

+ 만들어진 파드를 cat으로 작동이 되는지 확인

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_curl.png" alt="drawing" width="500"/>

+ 네트워크 파드를 생성해서 IP주소로도 나오는지 확인

### 초기화 컨테이너

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_init.png" alt="drawing" width="500"/>

- `initContainers:` 를 사용해서 처음 컨테이너를 구성하는 스크립트를 사용하고 사라지는 컨테이너

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_init.png" alt="drawing" width="500"/>

+ 초기구성 단계가 지나고나서 본격 컨테이너가 작동한다.

### hostpath 볼륨

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_hp_yaml.png" alt="drawing" width="500"/>

+ `web_content`라는 디렉토리를 node1서버에 만들고 그 디렉토리를 볼륨으로 `yaml`파일을 작성

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_hp_create_error.png" alt="drawing" width="500"/>

+ 하나의 파드만 실행되고있는 상황이고 `kubectl describe`로 오류상황을 봤다

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_hp_create_error_describe.png" alt="drawing" width="500"/>

+ `describe`로 확인해보면 생성하는 노드에 해당 디렉토리가 없어서 생성이 안되고있다고한다.

+ 우리는 `node1`에 디렉토리를 생성했고 나머지 두개의 노드에는 생성하지않았다.

+ 파드를 생성할때 노드를 번갈아가면서 생성하기이다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_hp_yaml_node.png" alt="drawing" width="500"/>

+ `yaml`파일에 `spec`명령어에 `node`라는 명령어를 추가하고 그곳에 `node1`을 추가해준다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_emptyDir_hp_create.png" alt="drawing" width="500"/>

+ 정상적으로 두개의 파드가 실행되고있는것을 볼 수 있다.

+ **이처럼 `HostPath`는 네트워크 기반이 아니라 물리적인 스토리지라서 해당하는 노드스토리지 위치를 정확히 넣어주어야 오류없이 사용가능하다.**

+ 파드가 삭제될때 이 스토리지에 데이터는 외부용 스토리지라서 영향을 끼치지않는다.

### PV 및 PVC 볼륨
#### PV 및 PVC 소개


### 정적 볼륨 프로비저닝
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_pv%2Cpvc_create.png" alt="drawing" width="500"/>

+ PV에 `spec`부분에서 `capacity`은 스토리지에 공간을 얼마나 할당 받을지를 정하는것

+ `accessModes` 공유받는 폴더에 어떤 권한을줄지 정하는데 tp가지가 있다.
  + `ReadWriteOnce` : 하나의 파드만 읽기/쓰기 가능
  + `ReadWritemany` : 여러 파드 읽기/쓰기 가능
  + `ReadOnlumany`: 여러파드 읽기만 가능

+ `RECLAIM POLICY`는 회수에 3가지 방법를 말하는것
  + 유지(Retain) : PV리소스를 그대로 유지한다. PV리소스를 삭제하더라도 외부 스토리지를 사용하고 있다면 외부 스토리지의 데이터는 그대로 남아있다. 그러나 다른 PVC리소스가 사용 할 수 있는 것은 아니다. 관리자가 수동으로 볼륨을 회수
  
  + 삭제(Delete) : PVC 리소스가 삭제되면 PV 리소스도 같이 삭제되고, 연결되어 있는 외부 스토리지의 데이터를 삭제 할 수도 있다. 동적프로비저닝, AWS, GCP, Azure의 기본 정책이다.
  
  + 재활용(Recycle) : 스토리지의 데이터를 삭제하고 다른 PVC가 PV리소스를 사용가능 하도록 만들어준다. 현재 NFS 및 hostPath 볼륨만 지원한다.
  
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_rs_pvc.png" alt="drawing" width="500"/>

+ 레플리카셋에 `PVC`를 볼륨을 추가해서 만들었다. 만들어진 `PVC` 이름을 넣어주면 된다.

+ 
  
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_volume_delete_curl.png" alt="drawing" width="500"/>

### 동적 볼륨 프로비저닝
#### ceph
+ 통합형 스토리지이고 모든 형태에 데이터를 제공
  + Block
  + Object
  + file
+ Ceph는 기본적으으로 

 + c
 + 설치 하는법 출처: https://rook.io/docs/rook/v1.3/ceph-quickstart.html
 
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_ceph_create.png" alt="drawing" width="500"/>

+ `Cluster.yaml` 파일이 빈디스크를 찾아서 하나로 올리고 스토리지로 사용

+ `Cluster.yaml` 이 클러스터를 관리할 수 있는 `MON`을 구성함

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_ceph_RBD_storageclass.png" alt="drawing" width="500"/>

+ `Storageclass.yaml`으로 Ceph 블록스토리지를 구성함


<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_ceph.png" alt="drawing" width="500"/>

+ `mds` 는 `filesysyem.yaml`으로 구성 할 수있다.

+ `MON` 은 `Cluster.yaml`으로 구성하는것

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Container_Kubernetes_ceph_tools.png" alt="drawing" width="500"/>

+ 
<img src="
