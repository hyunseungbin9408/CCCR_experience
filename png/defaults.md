#cloud-config
runcmd:
 - [yum, install, -y, httpd]
 - [systemctl, start, httpd]
 - [systemctl, enable, httpd]
 - [firewall-offline-cmd, --add-service=http]
 - [systemctl, restart, firewalld]
 - [yum, -y, install, https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm]
 - [yum, -y, install, https://rpms.remirepo.net/enterprise/remi-release-7.rpm]
 - [yum, -y, install, yum-utils]
 - [yum-config-manager, --enable, remi-php74]
 - [yum, -y, update]
 - [yum, install, -y, php*]
yum_repos:
  epel-testing:
    baseurl: http://yum.mariadb.org/10.4/rhel7-amd64
    enabled: true
    failovermethod: priority
    gpgcheck: true
    gpgkey: https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
    name: MariaDB
 - [yum, install, -y, MariaDB]
 - [systemctl, start, mariadb]
 - [systemctl, enable, mariadb]
 - [yum, -y, install, wget]
 - [wget, "http://wordpress.org/latest.tar.gz"]
 - [tar -xvzf latest.tar.gz -C /var/www/html]
 - [mysql, -u, root, -e, "CREATE, DATABASE, wordpress;"]
 - [mysql, -u, root, -e, "GRANT ALL ON wordpress.* TO 'student'@'localhost' IDENTIFIED BY 'dkagh1.';"]
 
