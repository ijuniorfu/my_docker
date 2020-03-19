FROM php:7.4-cli-alpine

MAINTAINER junior <ijuniorfu@gmail.com>

RUN sed -i -e 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories \
&& apk update \
&& apk add supervisor && mkdir /etc/supervisor.d \
&& apk add m4 autoconf make gcc g++ linux-headers php7-pecl-mcrypt
WORKDIR /tmp
RUN wget http://pecl.php.net/get/swoole-4.4.16.tgz && ls -al && tar -zxf swoole-4.4.16.tgz
WORKDIR /tmp/swoole-4.4.16
RUN phpize && ./configure && make && make install
RUN docker-php-ext-enable swoole  && docker-php-ext-install pdo_mysql
