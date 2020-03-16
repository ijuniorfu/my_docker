FROM ubuntu:bionic

MAINTAINER junior <ijuniorfu@gmail.com>

# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update

RUN apt-get install -y software-properties-common \
    language-pack-en-base

RUN LC_ALL=en_US.UTF-8
RUN cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y curl wget telnet supervisor vim net-tools \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    # Install PHP libraries
    # php7.4-mcrypt not support and move to PECL. Use extension Sodium: http://php.net/manual/book.sodium.php
    && apt-get install -y curl php7.4-fpm php7.4-cli php7.4-readline php7.4-mbstring php7.4-zip php7.4-intl php7.4-json php7.4-xml php7.4-curl php7.4-gd php7.4-pdo php7.4-mcrypt php7.4-imagick php7.4-imagick php7.4-mysql php7.4-redis php-mongodb php-pear php-memcache \
    # Install composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apt-get install -y nginx