# Ansible AWX를 이용해서 워드프레스 구축 실습

                                    ( ubuntu haproxy 2대 , wordpress 2대, mariadb 2대) 


### Galera mysql

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5fad5191-984e-4e07-b19f-1f2c3104e076/Mysql_galera_cluster.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5fad5191-984e-4e07-b19f-1f2c3104e076/Mysql_galera_cluster.png)

Galera replication 은 mysql(mariadb) 클러스터에 데이터들을 실시간으로 동기방식의 복제를 시켜주는 구조이다.

각각의 노드가 있고 아무 노드에 업데이트가 발생하면 모든 노드에 데이터를 복사를 하고 완료가 되면 업데이트 데이터를 저장한다.

wsrep 이 이러한 galera replication 에 노드들에 업데이트가 있을때마다 나머지 노드들에게 복사를 하고 업데이트 데이터를 저장하는 역할을 하는 모듈이다. 

galera cluster는 mysql (mariadb)이 버전이 다르더라도 같은 클러스터로 구성 할 수 있다.

## galera cluster 구성

galera mariadb구성 yaml파일과 j2파일이다.

데이터 베이스 그룹을 wp-db로 구성하였고 

galera는 mariadb 패키지와 같이 설치된다.

galera conf 파일 구성은  `bind-address={{ node1_ip }}` 에 실행하는 노드의 ip를 넣어주고  wsrep 모듈의 위치는 `/usr/lib64/galera-4/libgalera_smm.so` 명시를 해준다.

그 후에 galera 클러스터에 이름과 클러스터들의 ip주소들을 

`wsrep_cluster_address="gcomm://{{ node1_ip }},{{ node2_ip }}"` 로 클러스터를 구성하려고하는 노드들의 ip 주소를 다 적어주면된다.

[galera.yaml](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/05f04c49-7742-43c8-bca5-e89b36f1608a/galera.yaml)

```jsx
[mysqld]
binlog_format=ROW
default-storage-engine=innodb
innodb_autoinc_lock_mode=2
bind-address={{ db1_ip }}

[galera]
wsrep_on=1
wsrep_provider=/usr/lib64/galera-4/libgalera_smm.so 
wsrep_cluster_name="wp_wsrep_cluster"
wsrep_cluster_address="gcomm://{{ db1_ip }},{{ db2_ip }}"
wsrep_node_name={{ hostname }}
wsrep_node_address={{ db1_ip }}
wsrep_sst_method=rsync
```

# AWX 구성

AWX 는 Ansible 언어를 운영하는 미들웨어의 성격을 가지고있고 playbook이 없으면 할 수 있는 일이 거의없다.

## AWX Playbook

### inventory 구성

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57b365a2-e5bd-4c72-969a-2658ac1fe410/Screenshot_from_2020-08-14_17-07-34.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57b365a2-e5bd-4c72-969a-2658ac1fe410/Screenshot_from_2020-08-14_17-07-34.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/efc5716b-2e02-49d9-91bf-2fdbaa1ab81e/Screenshot_from_2020-08-14_17-07-47.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/efc5716b-2e02-49d9-91bf-2fdbaa1ab81e/Screenshot_from_2020-08-14_17-07-47.png)

인벤토리에 wp라는 큰 그룹을 생성하고 그 밑으로 세부적인 wp-db wp-web wp-lb이렇게 생성하였다.

그 후에 각각 db1,2 wp1,2 ha1,2 를 그룹에 호스트로 지정함으로써 이번 실습에 인벤토리를 구성하였다.

### Template 구성

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2212cc0-f837-4ecf-a6e4-b8106c539caf/Screenshot_from_2020-08-14_17-11-14.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2212cc0-f837-4ecf-a6e4-b8106c539caf/Screenshot_from_2020-08-14_17-11-14.png)

플레이북 파일은 roles 형식으로 구성하였고 

db 1,2 가  j2파일 형식이 다른데 block 과 when방식이 아직은 익숙하지않아서 일단 급하게 폴더를 두개로 나눠서 진행하였다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccb44b05-748d-4839-9a76-569f2e889ba3/Screenshot_from_2020-08-14_17-25-21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccb44b05-748d-4839-9a76-569f2e889ba3/Screenshot_from_2020-08-14_17-25-21.png)

템플릿에서 로켓모양을 클리하면 러닝이 된다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/566f6569-da0a-45ee-bf43-6e1a497abe44/Screenshot_from_2020-08-14_17-24-36.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/566f6569-da0a-45ee-bf43-6e1a497abe44/Screenshot_from_2020-08-14_17-24-36.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78e2a47a-a619-4049-8bd2-c4d49cef78dc/Screenshot_from_2020-08-14_17-04-43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78e2a47a-a619-4049-8bd2-c4d49cef78dc/Screenshot_from_2020-08-14_17-04-43.png)

이런식으로 db1에서 생성된 wordpress라는 데이터베이스를 db2에서 동기화된것을 확인 할 수 있다.

앞으로 실행을 하고있지만 작은 오류들이 많고 처리를 하고 업데이트를 할 예정입니다.
