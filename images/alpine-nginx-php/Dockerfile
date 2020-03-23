FROM alpine

MAINTAINER junior <ijuniorfu@gmail.com>

RUN sed -i -e 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories \
&& apk update \
&& apk add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone && apk del tzdata \
&& apk add nginx && mkdir /run/nginx \
&& apk add supervisor && mkdir /etc/supervisor.d \
&& apk add curl php7 php7-pcntl php7-openssl php7-tokenizer php7-pdo_mysql php7-fpm php7-pecl-imagick php7-mysqlnd php7-pecl-redis php7-pecl-amqp php7-opcache php7-curl php7-gd php7-mbstring php7-mysqli php7-json php7-mbstring php7-pecl-mcrypt php7-bcmath php7-pecl-igbinary php7-pecl-memcached php7-iconv php7-xml php7-zip \
&& rm -rf /tmp/* /var/cache/apk/*
