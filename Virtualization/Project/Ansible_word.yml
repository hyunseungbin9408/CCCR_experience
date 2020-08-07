---
- hosts: apache
  become: yes
  vars:
    http_port: 80
    max_client: 200
  remote_user: student
  tasks: 
  - yum:
      name: libsemanage-python
      state: latest
  - seboolean:
      name: httpd_can_network_connect_db
      state: yes
      persistent: yes
  - name: epel repository
    yum: 
      name: epel-release 
      state: latest
  - name: apache is at the latest version
    yum: 
      name: httpd 
      state: latest
    notify:
    - restart apache
  - name: php 7.4 version RPM
    yum:
      name: https://rpms.remirepo.net/enterprise/remi-release-7.rpm 
      state: latest
  - name: php 7.4 Download
    yum: 
      enablerepo: remi-php74 
      name: php 
      state: present
  - name: php-mysqlnd 7.4 Download
    yum: 
      enablerepo: remi-php74 
      name: php-mysqlnd 
      state: present
  - name: ensure apache is running
    service: 
      name: httpd 
      state: started 
      enabled: yes
  - name: wget Download
    yum: 
      name: wget 
      state: present
  - name: wget url
    get_url: 
      url: https://ko.wordpress.org/latest-ko_KR.tar.gz 
      dest: /var/www/html/latest-ko_KR.tar.gz
  - name: tar unarchive
    unarchive: 
      src: /var/www/html/latest-ko_KR.tar.gz  
      dest: /var/www/html/ 
      remote_src: yes
  - name: wp-config
    copy: 
      src: /var/www/html/wordpress/wp-config-sample.php 
      dest: /var/www/html/wordpress/wp-config.php 
      remote_src: yes
  - name: modify wp-config
    replace: 
      path: /var/www/html/wordpress/wp-config.php 
      regexp: database_name_here 
      replace: wordpress_db
  - name: modify wp-config
    replace: 
      dest: /var/www/html/wordpress/wp-config.php 
      regexp: username_here 
      replace: admin
  - name: modify wp-config
    replace: 
      dest: /var/www/html/wordpress/wp-config.php 
      regexp: password_here 
      replace: dkagh1.
  - name: modify wp-config
    replace: 
      dest: /var/www/html/wordpress/wp-config.php 
      regexp: localhost 
      replace: 192.168.122.52
  - name:
    firewalld:
      service: http
      permanent: yes
      state: enabled 
      immediate: yes
  - name:
    service: 
      name: httpd
      state: restarted 
      enabled: true
      
    ---
    - hosts: db
  vars:
    mysql_port: 3306
    max_clients: 200
  remote_user: student
  tasks:
  - name: mariadb repo
    yum_repository:
      name: MariaDB 
      baseurl: http://mirror.yongbok.net/mariadb/yum/10.5/centos7-amd64
      gpgkey: http://mirror.yongbok.net/mariadb/yum/RPM-GPG-KEY-MariaDB 
      gpgcheck: 1
      description: MariaDB
  - name: install mariadb
    yum:
      name: MariaDB
      state: present
  - name: start mariadb
    service:
      name: mariadb
      state: started
      enabled: true
  - name: 
    yum:
      name: MySQL-python
      state: latest
  - name:   
    mysql_db:
      login_user: root
      login_password: dkagh1.
      db: test 
      state: absent
  - name:
    mysql_user:
      login_user: root
      login_password: dkagh1.
      name: ''
      host_all: yes
      state: absent
  - name:
    mysql_db:
      login_user: root
      login_password: dkagh1.
      name: wordpress_db
      state: present
  - name:
    mysql_user:
      login_user: root
      login_password: dkagh1.
      name: admin
      password: dkagh1.
      priv: wordpress_db.*:ALL,GRANT 
      host: '%'
      state: present
  - name:
    firewalld:
      service: mysql
      permanent: yes
      state: enabled
      immediate: yes
