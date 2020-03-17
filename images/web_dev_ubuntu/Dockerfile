FROM ijuniorfu/ubuntu-base

MAINTAINER junior <ijuniorfu@gmail.com>

RUN add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    # Install PHP libraries
    && apt-get install -y curl mcrypt php7.4-dev php7.4-fpm php7.4-cli php7.4-readline php7.4-mbstring php7.4-zip php7.4-intl php7.4-json php7.4-xml php7.4-curl php7.4-gd php7.4-pdo php7.4-imagick php7.4-imagick php7.4-mysql php7.4-redis php-mongodb php-pear php-memcache \
    && pecl install mcrypt-1.0.3 \
    && pecl install swoole \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apt-get install -y nginx