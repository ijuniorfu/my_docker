# Version 0.1

# 基础镜像
FROM centos:6.6

# 维护者信息
MAINTAINER ijuniorfu@gmail.com

# 镜像操作命令
RUN yum clean all && \
yum install -y yum-plugin-ovl && \
yum install epel-release -y && \
yum update -y && \
yum -y install ntp make openssl openssl-devel pcre pcre-devel libpng libpng-devel libjpeg-6b libjpeg-devel-6b freetype freetype-devel gd gd-devel zlib zlib-devel gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 && \
yum install -y nginx && \
rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm && \
yum -y install php71w php71w-pdo php71w-soap php71w-opcache php71w-mcrypt php71w-mbstring php71w-gd php71w-fpm php71w-cli php71w-mysqlnd php71w-pear php71w-pecl-imagick php71w-pecl-imagick-devel php71w-pecl-redis php71w-pecl-mongodb php71w-pecl-memcached php71w-pecl-xdebug php71w-imap php71w-devel php71w-bcmath php71w-pecl-apcu php71w-pecl-apcu-devel php71w-pecl-igbinary && \
chown -R nginx:nginx /var/lib/php/

RUN sed -i -e 's/user = apache/user = nginx/' /etc/php-fpm.d/www.conf && \
sed -i -e 's/group = apache/group = nginx/' /etc/php-fpm.d/www.conf && \
sed -i -e 's/short_open_tag = Off/short_open_tag = On/' /etc/php.ini

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
yum -y install git && \
yum -y install wget && \
yum -y install tar && \
yum -y install telnet && \
chkconfig --levels 235 php-fpm on && \
chkconfig --levels 235 nginx on


# 安装swoole扩展
WORKDIR /tmp
RUN wget https://github.com/swoole/swoole-src/archive/v1.9.12.tar.gz -O swoole-src-1.9.12.tar.gz && \
tar -zxf swoole-src-1.9.12.tar.gz
WORKDIR /tmp/swoole-src-1.9.12
RUN phpize && \
./configure && \
make && make install && \
touch /etc/php.d/swoole.ini && \
echo "; Enable swoole extension module" > /etc/php.d/swoole.ini && \
echo "extension=swoole.so" >> /etc/php.d/swoole.ini

# 安装phalcon扩展
RUN yum -y install re2c
WORKDIR /tmp
RUN git clone https://github.com/phalcon/cphalcon
WORKDIR /tmp/cphalcon/build
RUN ./install && \
touch /etc/php.d/swoole.ini && \
echo "; Enable phalcon extension module" > /etc/php.d/phalcon.ini && \
echo "extension=phalcon.so" >> /etc/php.d/phalcon.ini

# 安装php7的memcache扩展
WORKDIR /tmp
RUN git clone https://github.com/websupport-sk/pecl-memcache memcache
WORKDIR /tmp/memcache
RUN phpize && \
./configure && \
make && make install && \
touch /etc/php.d/memcache.ini && \
echo "; Enable memcache extension module" > /etc/php.d/memcache.ini && \
echo "extension=memcache.so" >> /etc/php.d/memcache.ini


# 安装rabbitmq-c
#WORKDIR /tmp
#RUN wget https://github.com/alanxz/rabbitmq-c/archive/v0.8.0.tar.gz -O rabbitmq-c-0.8.0.tar.gz && \
#tar -zxf rabbitmq-c-0.8.0.tar.gz
#WORKDIR /tmp/rabbitmq-c-0.8.0
#RUN yum install -y libtool && autoreconf -i && \
#./configure --prefix=/usr/local/rabbitmq-c && \
#make && make install

# 安装amqp
#WORKDIR /tmp
#RUN wget http://pecl.php.net/get/amqp-1.9.0.tgz && \
#tar -zxf amqp-1.9.0.tgz
#WORKDIR /tmp/amqp-1.9.0
#RUN phpize && \
#./configure --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq-c && \
#make && make install && \
#touch /etc/php.d/amqp.ini && \
#echo "; Enable amqp extension module" > /etc/php.d/amqp.ini && \
#echo "extension=amqp.so" >> /etc/php.d/amqp.ini

# composer安装
RUN  curl -s http://getcomposer.org/installer | php && \
mv composer.phar /usr/bin/composer

ENV ROOT_PASSWORD 123456

# ssh安装
RUN yum install openssh-server -y && \
sed -i '$a PermitRootLogin yes' /etc/ssh/ssh_config && \
sed -i '$a UsePAM no' /etc/ssh/ssh_config && \
echo $ROOT_PASSWORD | passwd root --stdin && \
chkconfig --levels 235 sshd on && \
rm -rf /tmp/*


WORKDIR /

# 容器启动命令
CMD ["/sbin/init"]