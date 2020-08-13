# MYSQL 구성도
<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Mysql_logo.png" alt="drawing" width="500"/>

## mysql_replication

## mysql_galera

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Mysql_galera.png" alt="drawing" width="1000"/>

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Mysql_galera_cluster.png" alt="drawing" width="600"/>

데이터를 실시간으로 동기화를 시키는것을 `r(remote)sync`라고 한다.

`rsync`는 내부적으로 `ssh`를 사용하기 때문에 안전하게 사용가능하다.

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Mariadb_galerarepo.png" alt="drawing" width="500"/>
`MariaDB 10.4 repository` 패키지에 `Galera`도 포함되어있어서 레포를 등록하고 패키지를 설치하면된다.

`yum install -y policycoreutils-python`

방화벽을 열어준다
```
firewall-cmd --permanent --add-port=3306/tcp

firewall-cmd --permanent --add-port=4444/tcp

firewall-cmd --permanent --add-port=4567/tcp

firewall-cmd --permanent --add-port=4567/udp

firewall-cmd --permanent --add-port=4568/tcp
```
`systemctl stop mariadb`

`galera_new_cluster`

