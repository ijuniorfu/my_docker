
# 基础镜像
FROM ijuniorfu/centos7-systemd

# 维护者信息
MAINTAINER ijuniorfu@gmail.com

# 镜像操作命令
RUN yum clean all && \
yum makecache && \
yum update -y && \
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
yum -y install ntp make openssl openssl-devel pcre pcre-devel libpng libpng-devel libjpeg-6b libjpeg-devel-6b freetype freetype-devel gd gd-devel zlib zlib-devel gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 && \
yum install -y nginx && \
yum -y install php73-php-fpm php73-php-cli php73-php-pdo php73-php-soap php73-php-opcache php73-php-mcrypt php73-php-mbstring php73-php-gd php73-php-fpm php73-php-cli php73-php-mysqlnd php73-php-pear php73-php-pecl-imagick php73-php-pecl-imagick-devel php73-php-pecl-redis php73-php-pecl-mongodb php73-php-pecl-memcached php73-php-pecl-xdebug php73-php-imap php73-php-devel php73-php-bcmath php73-php-pecl-apcu php73-php-pecl-apcu-devel php73-php-pecl-igbinary && \
sed -i -e 's/user = apache/user = root/' /etc/php-fpm.d/www.conf && \
sed -i -e 's/group = apache/group = root/' /etc/php-fpm.d/www.conf

RUN  yum -y install kde-l10n-Chinese && \
yum -y reinstall glibc-common && \
localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 && \
echo "export LANG=zh_CN.UTF-8" >> /etc/profile && \
echo "export LC_ALL=zh_CN.UTF-8" >> /etc/profile && \
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
yum -y install git && \
yum -y install wget && \
yum -y install tar && \
yum -y install telnet && \
yum -y install net-tools && \
yum -y install crontabs && \
systemctl enable crond.service && \
systemctl enable php-fpm.service && \
systemctl enable nginx.service && \
sed -i -e 's/php-fpm --nodaemonize/php-fpm -R --daemonize/' /usr/lib/systemd/system/php-fpm.service

ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8

# 安装swoole扩展
WORKDIR /tmp
RUN wget http://pecl.php.net/get/swoole-4.4.12.tgz && \
tar -zxf swoole-4.4.12.tgz
WORKDIR /tmp/swoole-4.4.12
RUN phpize && \
./configure && \
make && make install && \
touch /etc/php.d/swoole.ini && \
echo "; Enable swoole extension module" > /etc/php.d/swoole.ini && \
echo "extension=swoole.so" >> /etc/php.d/swoole.ini

# 安装php7的memcache扩展
WORKDIR /tmp
RUN git clone https://github.com/websupport-sk/pecl-memcache.git
WORKDIR /tmp/pecl-memcache
RUN phpize && \
./configure && \
make && make install && \
touch /etc/php.d/memcache.ini && \
echo "; Enable memcache extension module" > /etc/php.d/memcache.ini && \
echo "extension=memcache.so" >> /etc/php.d/memcache.ini


# 安装rabbitmq-c
WORKDIR /tmp
RUN wget https://github.com/alanxz/rabbitmq-c/archive/v0.9.0.tar.gz -O rabbitmq-c-0.9.0.tar.gz && \
tar -zxf rabbitmq-c-0.9.0.tar.gz
WORKDIR /tmp/rabbitmq-c-0.9.0
RUN yum install -y libtool && autoreconf -i && \
./configure --prefix=/usr/local/rabbitmq-c && \
make && make install

# 安装amqp
WORKDIR /tmp
RUN wget http://pecl.php.net/get/amqp-1.9.4.tgz && \
tar -zxf amqp-1.9.4.tgz
WORKDIR /tmp/amqp-1.9.4
RUN phpize && \
./configure --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq-c && \
make && make install && \
touch /etc/php.d/amqp.ini && \
echo "; Enable amqp extension module" > /etc/php.d/amqp.ini && \
echo "extension=amqp.so" >> /etc/php.d/amqp.ini

# composer安装
RUN  curl -s http://getcomposer.org/installer | php && \
mv composer.phar /usr/bin/composer

ENV ROOT_PASSWORD 123456

# ssh安装
RUN yum install openssh-server -y && \
echo $ROOT_PASSWORD | passwd root --stdin && \
systemctl enable sshd.service && \
rm -rf /tmp/*

WORKDIR /

# centos7 容器启动命令
CMD ["/usr/sbin/init"]
