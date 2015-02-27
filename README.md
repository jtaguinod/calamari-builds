# calamari-builds
*Gather dependencies for the calamari-server

Some ubuntu repositories is not updated. THis repo works for me (http://archive.ubuntu.com/ubuntu/ trusty main)
echo "deb http://ppa.launchpad.net/saltstack/salt/ubuntu trusty main" | sudo tee /etc/apt/sources.list.d/saltstack.list
wget -q -O- "http://keyserver.ubuntu.com:11371/pks/lookup?op=get&search=0x4759FA960E27C0A6" | sudo apt-key add -
apt-get update
apt-get install salt-master salt-minion salt-syndic
echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
7)  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
8)  apt-get update && sudo apt-get upgrade
9)  apt-get install -y curl build-essential openssl libssl-dev apache2 libapache2-mod-wsgi libcairo2 supervisor \
    python-cairo libpq5 postgresql python-m2crypto python-virtualenv git python-dev swig libzmq-dev g++ postgresql-9.1 \
    postgresql-server-dev-9.1 libcairo2-dev python-pip libpq-dev ruby debhelper python-mock python-configobj \
    cdbs gem ruby1.9.1 ruby1.9.1-dev make devscripts software-properties-common python-support
10) dpkg -i calamari-server_1.0.0-1_amd64.deb
11) calamari-ctl initialize
12) cd calamari-clients
13) cp -avr dashboard/dist /opt/calamari/webapp/content/dashboard
14) cp -avr login/dist /opt/calamari/webapp/content/login
15) cp -avr manage/dist /opt/calamari/webapp/content/manage
16) cp -avr admin/dist /opt/calamari/webapp/content/admin 

Gather dependencies for calamari-clients - Do this to all ceph nodes!
1)  Some ubuntu repositories is not updated. THis repo works for me (http://archive.ubuntu.com/ubuntu/ trusty main)
2)  apt-get update
3)  apt-get install python-support
4)  echo "deb http://ppa.launchpad.net/saltstack/salt/ubuntu trusty main | sudo tee /etc/apt/sources.list.d/saltstack.list
5)  wget -q -O- "http://keyserver.ubuntu.com:11371/pks/lookup?op=get&search=0x4759FA960E27C0A6" | sudo apt-key add -
6)  apt-get update
7)  dpkg -i diamond_3.1.0_all.deb
8)  cp /etc/diamond/diamond.conf.example /etc/diamond/diamond.conf
9)  apt-get install salt-master salt-minion salt-syndic salt-cloud salt-ssh salt-api
10) echo "master: calamari" | sudo tee /etc/salt/minion.d/calamari.conf (NOTE: format should be "master: <hostname>")
11) check that hostname is properly resolved in /etc/hosts
12) service salt-minion restart
13) service diamond restart

Authorize Ceph cluster in calamari-server
1) salt-key -L (This should list all ceph-nodes)
2) salt-key -A (Press Y to accept all keys)
3) salt-key -L (This should list all accepted keys)

Your dashboard should be working now!
