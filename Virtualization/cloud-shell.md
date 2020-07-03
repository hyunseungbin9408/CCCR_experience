# 쉘 스크립트로 자동화

#!/bin/bash

setenforce 0
echo "[MariaDB]" > /etc/yum.repos.d/MariaDB.repo
echo "baseurl = http://yum.mariadb.org/10.4/rhel7-amd64" >> /etc/yum.repos.d/MariaDB.repo
echo "enabled = true" >> /etc/yum.repos.d/MariaDB.repo
echo "gpgcheck: true" >> /etc/yum.repos.d/MariaDB.repo
echo "gpgkey: https://yum.mariadb.org/RPM-GPG-KEY-MariaDB" >> /etc/yum.repos.d/MariaDB.repo
echo "name: MariaDB" >> /etc/yum.repos.d/MariaDB.repo
yum install -y httpd
systemctl start httpd
systemctl enable httpd
yum -y install "https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm"
yum -y install "https://rpms.remirepo.net/enterprise/remi-release-7.rpm"
yum -y install yum-utils
yum-config-manager --enable remi-php74
yum install -y php php-mysqlnd
systemctl restart httpd
yum install -y MariaDB
systemctl start mariadb
systemctl enable mariadb
mysql -u root -e "CREATE DATABASE wordpress;"
mysql -u root -e "GRANT ALL ON wordpress.* TO 'student'@'%' IDENTIFIED BY 'dkagh1.';"
yum -y install wget
wget "http://wordpress.org/latest.tar.gz" -P /root
tar -xvzf /root/latest.tar.gz -C /var/www/html
chown -R apache: /var/www/html/wordpress
