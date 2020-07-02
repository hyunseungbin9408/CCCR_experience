
#cloud-config
yum_repos:
  MariaDB:
    baseurl: http://yum.mariadb.org/10.4/rhel7-amd64
    enabled: true
    gpgcheck: true
    gpgkey: https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
    name: MariaDB
runcmd:
 - [ yum, install, -y, httpd ]
 - [ systemctl, start, httpd ]
 - [ systemctl, enable, httpd ]
 - [ firewall-offline-cmd, --add-service=http ]
 - [ systemctl, restart, firewalld ]
 - [ yum, -y, install, "https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm" ]
 - [ yum, -y, install, "https://rpms.remirepo.net/enterprise/remi-release-7.rpm" ]
 - [ yum, -y, install, yum-utils ]
 - [ yum-config-manager, --enable, remi-php74 ]
 - [ yum, -y, update ]
 - [ yum, install, -y, php, php-mysqlnd ]
 - [ systemctl, restart, httpd ]
 - [ yum, install, -y, MariaDB ]
 - [ systemctl, start, mariadb ]
 - [ systemctl, enable, mariadb ]
 - [ mysql, -u, root, -e, "CREATE DATABASE wordpress;" ]
 - [ mysql, -u, root, -e, "GRANT ALL ON wordpress.* TO 'student'@'localhost' IDENTIFIED BY 'dkagh1.';" ]
 - [ yum, -y, install, wget ]
 - [ wget, "http://wordpress.org/latest.tar.gz", -P, /root ]
 - [ tar, -xvzf, /root/latest.tar.gz, -C, /var/www/html ]
 
