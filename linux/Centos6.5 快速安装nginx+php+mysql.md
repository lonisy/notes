Centos6.5 快速安装nginx+php+mysql
========================================


网站服务器账号信息    
登录名: root   
登录密码:      

mysql: root    
密码:   

线上网站程序目录    
所在目录: /data    

服务器安装软件清单    
nginx, php5.6 php-fpm mysql5.6  phalcon扩展      

防火墙配置    
仅开放  ssh  和 web 端口  

```

# 免除登录

# 本地复制公钥到服务器
scp .ssh/id_rsa.pub USER@IP:~/id_rsa.pub

mkdir .ssh
cat id_rsa.pub >> .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
rm -rf id_rsa.pub



# 安装nginx
yum info nginx
vim /etc/yum.repos.d/nginx.repo

[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/6/$basearch/
gpgcheck=0
enabled=1

yum -y install nginx
service nginx start
chkconfig --level 3 nginx on
rm -rf /etc/yum.repos.d/nginx.repo

# nginx 日志自动切割配置
yum -y install logrotate crontabs
vim /etc/logrotate.d/nginx
logrotate -f /etc/logrotate.d/nginx



# 安装 MySQL5.6
wget http://dev.mysql.com/get/mysql57-community-release-el6-8.noarch.rpm
yum -y localinstall mysql57-community-release-el6-8.noarch.rpm
vim /etc/yum.repos.d/mysql-community.repo

# Enable to use MySQL 5.6 启用 MySQL5.6
[mysql56-community]
name=MySQL 5.6 Community Server
baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
enabled=1(这里)
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

[mysql57-community]
name=MySQL 5.7 Community Server
baseurl=http://repo.mysql.com/yum/mysql-5.7-community/el/6/$basearch/
enabled=0
gpgcheck=1

yum -y install mysql-community-server
service mysqld start
/usr/bin/mysql_secure_installation
mysql -u root -p
chkconfig --level 3 mysqld on
rm -rf /etc/yum.repos.d/mysql-community.repo

# 安装 php5.6
yum list installed | grep php # 查看已安装的PHP相关软件
rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm
yum list php56* # 查看可以安装的软件列表

yum -y install php56w.x86_64 php56w-cli.x86_64 php56w-common.x86_64 php56w-gd.x86_64 php56w-ldap.x86_64 php56w-mbstring.x86_64 php56w-mcrypt.x86_64 php56w-mysql.x86_64 php56w-pdo.x86_64 php56w-fpm

yum -y install php56w-devel

yum -y install php56w.x86_64 php56w-cli.x86_64 php56w-common.x86_64 php56w-gd.x86_64 php56w-ldap.x86_64 php56w-mbstring.x86_64 php56w-mcrypt.x86_64 php56w-mysql.x86_64 php56w-pdo.x86_64 php56w-fpm php56w-devel

chkconfig --level 3 php-fpm on
service php-fpm start

yum -y install php56w-pecl-memcache php56w-pecl-memcached php56w-pecl-redis

# php56w-pecl-imagick.x86_64
# php56w-pecl-imagick-devel.x86_64
# php56w-pecl-memcache.x86_64
# php56w-pecl-memcached.x86_64
# php56w-pecl-redis.x86_64

# 安装 phalcon 扩展
yum -y install pcre-devel gcc make # 另需要提前安装 php-devel
wget https://github.com/phalcon/cphalcon/archive/phalcon-v2.0.8.zip
unzip phalcon-v2.0.8.zip
cd cphalcon-phalcon-v2.0.8/build/
./install

# 启用phalcon 扩展
cd /etc/php.d/
cp gd.ini phalcon.ini
# vim phalcon.ini
service php-fpm restart


# 启用 phpinfo 页面
cd /usr/share/nginx/html
echo "<?php phpinfo(); ?>" > phpinfo.php

# 编辑nginx 默认配置
vim /etc/nginx/conf.d/default.conf
service nginx restart

# 相关命令
chkconfig --level 3 php-fpm on
service php-fpm start
service mysqld start
php --version


# 安装 iptalbes 防火墙
service iptalbes status
yum -y install iptables
iptables -L -n
iptables -P INPUT ACCEPT
iptables -F
iptables -X
iptables -Z
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED -j ACCEPT
iptables -P INPUT DROP
iptables -L -n
service iptables save
chkconfig iptables on
service iptables start



# 安装 phalcon3.0 扩展
wget https://github.com/phalcon/cphalcon/archive/v3.0.0.zip
unzip v3.0.0.zip
cd cphalcon-3.0.0/build/
./install
cd /etc/php.d/
cp gd.ini phalcon.ini
# cat phalcon.ini #查看
echo "extension=phalcon.so" > phalcon.ini
# cat phalcon.ini #查看
service php-fpm start
```
