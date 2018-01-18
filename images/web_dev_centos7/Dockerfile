
# 基础镜像
FROM ijuniorfu/centos7-systemd

# 维护者信息
MAINTAINER ijuniorfu@gmail.com

# 镜像操作命令
RUN yum clean all && \
yum makecache && \
yum update -y && \
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
yum -y install ntp make openssl openssl-devel pcre pcre-devel libpng libpng-devel libjpeg-6b libjpeg-devel-6b freetype freetype-devel gd gd-devel zlib zlib-devel gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 && \
yum install -y nginx && \
yum -y install php71w php71w-pdo php71w-soap php71w-opcache php71w-mcrypt php71w-mbstring php71w-gd php71w-fpm php71w-cli php71w-mysqlnd php71w-pear php71w-pecl-imagick php71w-pecl-imagick-devel php71w-pecl-redis php71w-pecl-mongodb php71w-pecl-memcached php71w-pecl-xdebug php71w-imap php71w-devel php71w-bcmath php71w-pecl-apcu php71w-pecl-apcu-devel php71w-pecl-igbinary && \
chown -R nginx:nginx /var/lib/php/

RUN sed -i -e 's/user = apache/user = nginx/' /etc/php-fpm.d/www.conf && \
sed -i -e 's/group = apache/group = nginx/' /etc/php-fpm.d/www.conf

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
yum -y install git && \
yum -y install wget && \
yum -y install tar && \
yum -y install telnet && \
systemctl enable php-fpm.service && \
systemctl enable nginx.service

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