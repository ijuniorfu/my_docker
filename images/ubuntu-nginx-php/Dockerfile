FROM ijuniorfu/ubuntu-base

MAINTAINER junior <ijuniorfu@gmail.com>

RUN add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    # Install PHP libraries
    && apt-get install -y mcrypt libmcrypt-dev php7.4-fpm php7.4-cli php7.4-dev php7.4-readline php7.4-mbstring php7.4-zip php7.4-intl php7.4-json php7.4-xml php7.4-curl php7.4-gd php7.4-pdo php7.4-mysql php-imagick php-redis php-mongodb php-memcache \
    && curl -s http://getcomposer.org/installer | php && mv composer.phar /usr/bin/composer \
    && apt-get install -y nginx

# 安装mcrypt扩展
WORKDIR /tmp
RUN wget https://pecl.php.net/get/mcrypt-1.0.3.tgz  \
    && tar -zxf mcrypt-1.0.3.tgz
WORKDIR /tmp/mcrypt-1.0.3
RUN phpize  &&  ./configure &&  make  && make install \
&& touch /etc/php/7.4/mods-available/mcrypt.ini \
&& echo "; Enable mcrypt extension module" > /etc/php/7.4/mods-available/mcrypt.ini \
&& echo "extension=mcrypt.so" >> /etc/php/7.4/mods-available/mcrypt.ini \
&& ln -s /etc/php/7.4/mods-available/mcrypt.ini /etc/php/7.4/cli/conf.d/20-mcrypt.ini \
&& ln -s /etc/php/7.4/mods-available/mcrypt.ini /etc/php/7.4/fpm/conf.d/20-mcrypt.ini

# 安装swoole扩展
WORKDIR /tmp
RUN wget http://pecl.php.net/get/swoole-4.4.16.tgz  \
    && tar -zxf swoole-4.4.16.tgz
WORKDIR /tmp/swoole-4.4.16
RUN phpize  &&  ./configure &&  make  && make install \
&& touch /etc/php/7.4/mods-available/swoole.ini \
&& echo "; Enable swoole extension module" > /etc/php/7.4/mods-available/swoole.ini \
&& echo "extension=swoole.so" >> /etc/php/7.4/mods-available/swoole.ini \
&& ln -s /etc/php/7.4/mods-available/swoole.ini /etc/php/7.4/cli/conf.d/20-swoole.ini \
&& ln -s /etc/php/7.4/mods-available/swoole.ini /etc/php/7.4/fpm/conf.d/20-swoole.ini

WORKDIR /
RUN rm -rf /tmp/mcrypt-1.0.3 \
&& rm -rf /tmp/mcrypt-1.0.3.tgz \
&& rm -rf /tmp/swoole-4.4.16 \
&& rm -rf /tmp/swoole-4.4.16.tgz

CMD service nginx start && service php7.4-fpm start