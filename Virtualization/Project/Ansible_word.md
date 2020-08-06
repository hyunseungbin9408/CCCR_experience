wordpress
ansible node1.cccr.com -i inventory -m selinux -a 'state=disabled' -b
ansible node1.cccr.com -i inventory -m yum -a 'name=httpd state=installed' -b
ansible node1.cccr.com -i inventory -m service -a 'name=httpd state=started' -b
ansible node1.cccr.com -i inventory -m yum -a "name=https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm state=present" -b
ansible node1.cccr.com -i inventory -m yum -a "name=https://rpms.remirepo.net/enterprise/remi-release-7.rpm state=present" -b
ansible node1.cccr.com -i inventory -m yum -a "name=yum-utils state=present" -b
ansible node1.cccr.com -i inventory -m yum -a "enablerepo=remi-php74 name=php state=present" -b
ansible node1.cccr.com -i inventory -m yum -a "enablerepo=remi-php74 name=php-mysqlnd state=present" -b
ansible node1.cccr.com -i inventory -m service -a "name=httpd state=restarted" -b
ansible node1.cccr.com -i inventory -m get_url -a 'url=http://wordpress.org/latest.tar.gz dest=/home/student/' -b
ansible node1.cccr.com -i inventory -m unarchive -a 'remote_src=yes src=/home/student/wordpress-5.4.2.tar.gz dest=/var/www/html' -b
ansible node1.cccr.com -i inventory -m file -a 'recurse=yes owner=apache path=/var/www/html/wordpress' -b
ansible node1.cccr.com -i inventory -m firewalld -a 'immediate=yes permanent=yes service=http state=enabled' -b

mariadb

ansible node2.cccr.com -i inventory -m yum_repository -a "description=mariadb10.4 name=MariaDB baseurl=http://yum.mariadb.org/10.4/rhel7-amd64 enabled=1 gpgcheck=1 gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB" -b
ansible node2.cccr.com -i inventory -m yum -a "name=MariaDB state=present" -b
ansible node2.cccr.com -i inventory -m service -a "name=mariadb state=started" -b
ansible -i inventory node2.cccr.com -m mysql_user -a "login_user=root login_password='' name=root host=localhost password=dkagh1. check_implicit_admin=yes" -b
