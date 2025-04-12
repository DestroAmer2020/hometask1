Hometask #1
- Create repo hometask1 (do not forget .gitignore)
- Create Vagrantfile
- Centos generic/centos9s
- Provision Nginx server
- Forward port 80 → 8888
- Push your project to github (and add user sko-lv as colaborator) Commands to install nginx on Centos:
  yum install -y epel-release
  yum install -y nginx
  setenforce 0
  sed -ie 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config cat /etc/selinux/config
  systemctl start nginx
  systemctl enable nginx
  systemctl disable firewalld
  systemctl stop firewalld
  Success criteria:
  vagrant up
  In your browser goto localhost:8888
  See content placed to ~/www-content (*)

## How to start:
1. vagrant up 
2. visit http://localhost:8888/
