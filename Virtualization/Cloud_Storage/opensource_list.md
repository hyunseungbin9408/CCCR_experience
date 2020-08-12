# 클라우드 스토리지 개요 및 오픈소스 목록
## 클라우드 스토리지란?

`Ref. https://gomindsight.com/insights/blog/what-is-cloud-storage-overview-cloud-basics/`

 많은 서버가 온라인 저장소를 이용하여 정보를 저장하고 그 저장소는 호스팅 회사가 항상 유지를 한다. 호스트서비스는 인터넷을 이용해서 개인이나 단체가 데이터를 이 가상공간에 저장 할 수 있다.
 
 우리가 흔히 사용하는 `Microsoft office 365`와 `DropBox`, `GoogleDrive`가 클라우드 스토리지로 제공하는것이고 또한 미디어 공유장치처럼 인스타그램과 유튜브, 웹메일, gmail이 이 카테고리안에 들어간다.
 
 서로 다른 서비스들을 클라우드위에 저장 할 수 있다.

***

# 오픈소스 목록

## owncloud

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/owncloud_logo.png" alt="drawing" width="500"/>

`Ref. https://www.tecmint.com/install-owncloud-to-create-personal-storage-in-linux/`

`owncloud`는 오픈소스이며 강력한 데이터 동기화 어플리케이션이며, 파일공유, 기본적인 파일스토리지이다. `owncloud`는 `PHP/Javascript` 로 쓰여졌다. 다양한 데이터베이서 관리시스템을 포함된 작업환경이 구성되어있고, `MYSQL, MariaDB, SQLite, Oracle Database, PostgreSQL`을 포함한다. 

`owncloud`는 우리가 알고있는 모든 플랫폼에서 배포할수있다. `Linux, Macintosh, Widows, Android` 와 같은 운영체제에서도 가능하고 플랫폼에 의존성이 적다. 이용하기 쉬운 오픈소스 어플리케이션이다.

## 기능

파일, 폴더, 사진갤러리, 캘린더를 우리가 정한 저장소 서버에있고 나중에 모바일, 데스크탑이나 웹브라우저에서 접속 할 수 있다. 

사용자 인터페이스로 쉽게 관리, 업로드, 사용자 생성을 할 수 있다.

중요한 기능중 하나로 사용자가 실수로 지운 데이터를 휴지통에서 삭제취소를 할 수 있다.

쉽게 다른 `owncloud server`로 옮길 수 있다.

PDF viewer와 새로운버전인 PDF.js가 추가되었다.

사용자 관리, 기능 셋팅, 관리자 페이지가 있다.

***

## Nextcloud

파일 호스팅 서비스 및 생성을 위한 클라이언트서버 어플리케이션 오픈소스이다. 개인에서 엔터프라이즈까지 설치 가능한 소프트웨어이고 그들의 개인서버를 실행 할 수 있다.

***

## seafile

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/seafile_logo.png" alt="drawing" width="500"/>

`Ref. https://www.seafile.com/en/home/ `

오픈 소스 속성을 활용하여 사용자에게 좋은 클라우드 스토리지 소프트웨어 시스템에서 기대하는 모든 이점을 제공하는 또 다른 파일 호스팅 소프트웨어 시스템으로 C, python으로 2015년 10월 15일 4.4.3버전으로 출시

Seafile은 Windows, Linux, OS X를 위한 데스크탑 클라이언트와 Android, iOS 및 Windows Phone을 위한 모바일 클라이언트를 제공한다. 2012년 오픈한 이후로 주목받기 시작했다. **주요기능은 데이터 안전에 초점을 맞춘 동기화와 공유다.** 온라인 파일 편집, 필요한 대역폭을 최소화하기 위한 차등 동기화, 클라이언트 데이터 보안을 위한 클라이언트 측 암호화 등 많은 대학에서 일반화 됌

***

## Pydio

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/pydio_logo.png" alt="drawing" width="500"/>

`Ref. https://pydio.com/ `

파일 호스팅, 공유 및 동기화를 제공하는것을 목표로 하는 프리웨어다. 2009년 Charles du Ju에 의해 시작되었고 2010년 이후 LaCie가 공급하는 모든 NAS장비에 탑재

Pydio는 PHP와 JavaScript로 작성되었으며 Window, Mac OS, Linux와 iOS 및 Android에서도 사용 할 수 있다. 거의 50만 건의 소스 포지에 대한 다운로드와 Red Hat 및 Oracle과 같은 회사들의 수용으로 Pydio는 시장에서 가장 인기있는 클라우드 스토리지 소프트웨어 중 하나

Pydio는 웹 서버에서 실행되며 어떤 브라우저를 통해서도 접속 할 수 있는 코어이다. 통합된 WebDAV 인터페이스는 온라인 파일 관리에 이상적으로 만들고 SSL/TLS 암호화는 전송 채널을 암호화하여 데이터를 보호하고 사생활을 보장한다. 이 소프트웨어와 함께 제공되는 다른 기능으로는 구문 강조표시, 오디오 및 비디오 재생, Amazon, S3, FTP 또는 MySQL 데이터베이스의 통합, 이미지 편집기, 파일 또는 폴더 공유 등이 있다.

***

## Ceph

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ceph_logo.png" alt="drawing" width="500"/>

`Ref. https://ceph.io/`

Ceph는 처음에 Sage Well에 의해 박사학위 논문으로 시작되었고, 2007년 가을 이 프로젝트를 계속했고 개발팀을 확장했다. 2014년 4월 Red Hat은 자체 개발을 완료했다. 지금까지 8개의 Ceph가 2015년 4월 7일 Hammer로 출시되었다. Ceph는 C++ 및 Perl로 작성된 분산 클러스터로, 확장성이 뛰어나고 자유롭게 사용 가능

데이터는 아마존 S3 및 Openstack Swift API를 지원 할 수 있는 RADOS 게이트웨이를 통해 블록장치, 파일 또는 형식의 개체로 Ceph에 입력 할 수 있다. 데이터, 확장성 및 신뢰성 측명에서 보안성 외에도 Ceph가 제공하는 기능은 다음과 같다.

+ 고성능 및 대용량 데이터 스토리지를 목표로 하는 네트워크 파일 시스템

+ VM 클라이언트와의 호환성

+ 개체 수준 매핑

***

## Syncany

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Syncany_logo.png" alt="drawing" width="500"/>

`Ref. https://www.syncany.org/`

2014년 3월에 출시된 Syncany는 가장 가볍고 개방적인 소스 클라우드 스토리지 및 파일 공유 애플리케이션 중 하나이고 현재 필립 C에 의해 활발하게 개발되고 있다. 현재 Heckkel은 지원되는 모든 플랫폼에 대한 명령줄 도구로 사용가능

Syncany의 가장 중요한 특징 중 하나는 툴이며 FTP 또는 SFTP 스토리지, WebDAV 또는 Samba Shares, Amazon S3 버킷 등이 될 수 있는 자체 스토리지를 도입해야 한다.

로컬 컴퓨터에서 나가는 모든 데이터에 대한 128비트 AES+Twofish/GCM 암호화, 친구와 파일을 공유 할 수 있는 파일 공유 지원, 공급업체 기반 스토리지 대신 사용자가 선택한 오프사이트 스토리지, 2진수 호환 파일 버전g, 로컬 파일 중복 제거, 그것은 일부 제공 업체들이 제공하는 스토리지를 신롸하기 보다는 그들 자신의 스토리지 공간을 사용하기를 원하는 기업들에게 더 유리 할 수 있다.

***

## Cozy

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Cozy_logo.png" alt="drawing" width="500"/>

`Ref. https://cozy.io/en/`

파일 공유, 동기화 도구 또는 소프트웨어가 아닌 Cozy는 전체 앱 엔진을 구축하는 데 도움이 되는 기능의 완전한 패키지에 번들로 구성되어 있다.

Syncany처럼 Cozy는 스토리지 공간 측면에서 사용자에게 유연성을 제공한다. 자신만의 개인 스토리지를 사용하거나 Cozy 팀의 서버를 신회 할 수 있다. 데이터베이스 스토리지용 CouchDB와 인덱싱을 위한 woosh와 같은 완전한 기능을 위해 몇몇 오픈 소스 소프트웨어에 의존한다. 스마트폰을 포함한 모든 플랫폼에서 이용 가능하다.

클라우드 스토리지 소프트웨어를 반드시 보유해야 하는 주요 기능: 클라우드에 모든 연락처, 파일, 캘린더 등을 저장하고 노트북과 스마트폰 간에 동기화하는 기능, 저장소의 Git URL을 공유하거나, 정적 웹 사이트 또는 HTML5 비디오 게임 호스팅을 통해 사용자가 자신의 앱을 만들고 다른 사용자와 공유 할 수 있는 기능 콘솔등이 있다.

Cozy 팀은 저렴한 하드웨어에도 가용성을 제공하기 위한 한 걸음 더 나아가 Rasberry Pi, 소형 디지털 오션 VPS등과 같은 저렴한 하드웨어에서도 잘 작동하는 Cozy Light를 도입했다.

***

## GlusterFS

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Gluster_logo.png" alt="drawing" width="500"/>

`Ref. https://www.gluster.org/ `

GlusterFS는 네트워크 연결 파일 스토리지 시스템이다. 처음에 글러스터사가 시작한 이 프로젝트는 현재 Red Hat 사에 속해있다. 2011년 글러스터 사를 인수한 후 Red Hat 통합 Gluster FS와 Red Hat 스토리지 서버의 이름을 Red Hat Gluster Storage로 변경되었다. GPLv3에 따라 일부 라이센스가 부여된 Linux, OS X, NetBSd 및 OpenSolaris를 포함한 플랫폼에서 사용 할 수 있으며, 다른 일부 부품은 GPLv2에 따라 이중 라이센스가 부여된다. 학문적 연구의 토대로 사용되어 왔다.

GlusterFS는 서버를 스토리지 벽돌로 구축하는 클라이언트-서버 모델을 사용한다. 클라이언트는 TCP/IP, Infiband 또는 SDP를 통한 사용자 정의 프로토콜로 서버에 연결하여 파일을 GlusterFs 서버에 저장 할 수 있다. 파일 기반 미러링 및 복제, 파일 기반 스트라이핑, 로드 밸런싱, 스케줄링 및 Disk 캐싱 등 파일에 걸쳐 채택되고 있는 다양한 기능이 있다.

이것의 또 다른 매우 유용한 특징은 유연하다는 것이다. 즉, 여기 있는 데이터는 xfs, ext4 등과 같은 네이티브 파일 시스템에 저장된다.

***

## StackSync

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Stacksync_logo.png" alt="drawing" width="500"/>

`Ref. http://cloudlab.urv.cat/web/software/released-software/stacksync`

StackSync는 OpenStack swift에서 실행되는 Dropbox와 같은 툴로서, 한 곳에서 데이터를 동기화하는 조직의 요구사항을 해결하도록 특별히 설계되었다. 그것은 자바 언어로 작성되었고 GNU General Public License v3에 따라 발매되었다.
 
프레임워크는 동기화 서버, Openstakc swift, 데스크톱, 모바일 클라이언트 등 세 가지 주요 구성요소로 구성되어 있다. 서버가 메타데이터와 논리를 처리하는 동안 Openstack은 메타데이터를 저장하는 데 초점을 맞추고 있으며 데스크톱과 모바일 클라이언트는 사용자가 자신의 데이터를 개인 클라우드에 동기화 할 수 있다.
 
StackSync는 클라우드 리소스를 효율적으로 사용하여 수천 명의 사용자 요구를 충족하기 위해 확장 할 수 있도록 지원하는 다양한 데이터 최적화를 채택하고 있다. 다른 기능으로는 REST API를 Swift 모듈로 제공하여 모바일 애플리케이션 및 타사 애플리케이션이 데이터를 동기화 하는데 사용 할 수 있도록 지원, 다양한 구성을 기반으로 구축 시 유연하게 사용 할 수 있도록 하는 데이터와 메타데이터의 분리, 퍼블릭 클라우드 공급업체와 Private에 모두 유용한 공융 구성 제공등이 있다. 더 나은 클라우드 스토리지 솔루션을 지향하는 대기업의 문제를 해결하는 구성을 가진다.
 
***

## Git-annex

Git-annex는 2010년 10월에 발매된 Joey Hess가 개발한 또 다른 파일 동기화 서비스로서, 상업 서비스나 중앙 서버와는 무관하지만 파일 공유와 동기화 문제를 해결하기 위한 것이다. Haskell로 작성되었으며 Linux, Android, OS X 및 Windows에서 사용 할 수 있다

Git-anex는 세션을 다시 Git에 저장하지 않고 사용자의 Git 저장소를 관리한다. 그러나 대신 Git저장소의 파일에 대한 링크만 저장하고 링크와 관련된 파일을 별도의 위에 관리한다. 손실된 정보의 복구가 필요한 파일의 중복성을 보장한다.

또한, 필요할 때 즉시 파일 데이터의 가용성을 보장하여 각 시스템에 파일이 표시되는 것을 방지한다. 이것은 많은 메모리 오버헤드를 줄인다. 특시 Git-annex는 Fedora, Ubuntu, Debian 등 다양한 Linux 배포판에서 구입 할 수 있다.

***

## Yandex.Disk

Yandex.Disk는 2012년 4월에 출시된 클라우드 스토리지 및 동기화 서비스로 Linux, Windows, OS X, Android, iOS 및 Windows Phone을 포함한 모든 주요 플랫폼에서 이용 가능하다. 사용자들이 다른 장치들 간의 데이터를 동기화하고 온라인에서 다른 사람들과 공유 할 수 있게 해준다.

`Yandex` 가 제공하는 다양한 기능은 다음과 같다. 사용자가 노래를 미리 볼 수 있도록 하는 내장 플래시 플레이어, 다운로드 링크를 공유하여 파일공유, 동일한 사용자의 다른 장치간의 파일 동기화, 무제한 스토리지, WebDAV 프로토콜을 지원하는 모든 애플리케이션에서 파일을 쉽게 관리 할 수 있도록 지원하는 내장 플래시 플레이어 등이 있다.

***

## Bitcasa

캘리포니아에 본사를 둔 Bitcasa는 오픈 소스 클라우드 스토리지와 Windows, OS X, Android 및 Linux에서 사용 할 수 있는 동기화를 위한 또 다른 솔루션이다. 오픈소스 소프트웨어는 아니지만 gcc/clang, libCurl, OpenSSL, APR, Rapid JSON 등 오픈소스 소프트웨어를 많이 사용하는 오픈소스 커뮤니티의 일부분이다.

파일 스토리지가 주요 특징인 파일 스토리지로서, 전 세계  140여 개 국가의 고객들 사이에서 이 제품이 인기를 끌게하는 특징들을 공유하고 접속하는 것은 대부분 안전하다. 하지만 이와 관련된 위험으로 적은 통합 암호화 프로토콜, OEM을 위한 보안 API 및 화이트 라벨 스토리지 애플리케이션 제공 등이 있다.

***

## NAS4Free

NAS는 'Network Attached Storage'의 약자로, '4Free'는 무료 및 오픈소스 특성을 나타낸다. NAS4Free는 2012년 3월에 이 이름으로 출시되었다. PHP로 작성되고 SDD 라이선스로 출시되는 사용자 인터페이스를 갖춘 네트워크 연결 스토리지 서버 소프트웨어입니다. i386/IA-32와 x86-64를 포함한 플랫폼을 지원한다.

NAS4Free는 여러 운영체제 간의 공유를 지원한다. 또한, 여기에는 Samba, CARP, Bridge, FTP, RSYNC, TFTP, NFS와 같은 프로토콜을 포함한 ZFS, 디스크 암호화 등도 포함된다. 다른 소프트웨어와 달리 NAS4Free는 USB/SSD 키, 하드 디스크 또는 구성 스토리지용 소형 USB키를 사용하여 LiveCD, LiveUSB에서 부팅 할 수 있다.


