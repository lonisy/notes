# Centos6.5 安装 nginx mysql php 

## 配置免密码登录

```shell
ssh root@ip 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```

## 安装 nginx

```shell
yum -y install nginx  
chkconfig --level 3 nginx on  
service nginx start  

vim /etc/nginx/conf.d/default.conf   
/\#去掉  listen  [::]:80 default_server;  

yum -y install logrotate crontabs     
logrotate -f /etc/logrotate.d/nginx    
```

## 安装 php5.6 php-fpm
```shell
yum list installed | grep php  
yum list php56*  
rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm  
yum -y install php56w.x86_64 php56w-cli.x86_64 php56w-common.x86_64 php56w-gd.x86_64 php56w-ldap.x86_64 php56w-mbstring.x86_64 php56w-mcrypt.x86_64 php56w-mysql.x86_64 php56w-pdo.x86_64 php56w-fpm php56w-devel  
yum -y install php56w-pecl-imagick php56w-pecl-imagick-devel  

// Mysql连接多编码支持
yum erase php56w-mysql -y
yum -y install php56w-mysqlnd

// 修改时区  
sed -ie 's/\;date\.timezone\ =/date\.timezone\ =\ Asia\/Shanghai/g' /etc/php.ini   
chkconfig --level 3 php-fpm on  
service php-fpm start  

vim /etc/php.ini

[projectenv]
run.env = dev

```


## 安装 phalcon 3.0
```shell
wget https://codeload.github.com/phalcon/cphalcon/zip/v3.0.0  
unzip v3.0.0  
cd cphalcon-3.0.0/  
cd build/  
./install  
cd /etc/php.d/  
cp gd.ini phalcon.ini  
echo "extension=phalcon.so" > phalcon.ini  
service php-fpm restart  
```

## 安装 mysql5.7
```shell
wget http://dev.mysql.com/get/mysql57-community-release-el6-8.noarch.rpm   
yum -y localinstall mysql57-community-release-el6-8.noarch.rpm  
yum -y install mysql-community-server  
chkconfig --level 3 mysqld on
service mysqld start
rm -rf /etc/yum.repos.d/mysql-community.repo
```
## 安装 iptables
```shell
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
```
## 其他
```shell
ps -ef|grep mysql // 查询mysql运行状态,查看日志位置
cat /var/log/mysqld.log | grep "temporary password" // 查询初始密码
/usr/bin/mysql_secure_installation // 重置mysql 

// date.timezone = Asia/Shanghai  
```