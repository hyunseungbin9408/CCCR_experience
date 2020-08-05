ansible node1.cccr.com -i inventory -m selinux -a 'state=disabled' -b
ansible node1.cccr.com -i inventory -m yum -a 'name=httpd state=installed' -b
ansible node1.cccr.com -i inventory -m service -a 'name=httpd state=started' -b
ansible node1.cccr.com -i inventory -m yum -a "name=https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm state=present" -b
