FROM php:8.3-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        $PHPIZE_DEPS \
        git \
        vim \
        zip \
        unzip \
        patch \
      bash-completion \
      libicu-dev \
      default-mysql-client \
      libldap2-dev \
      imagemagick \
      libmagickwand-dev \
      libyaml-dev \
      libonig-dev \
      libzip-dev \
      openssh-client \
      procps \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd pdo
RUN docker-php-ext-install -j$(nproc) intl \
    pdo_mysql \
    mbstring \
    exif \
    opcache \
    ldap \
    shmop \
    bcmath \
    sockets \
    gettext \
    sysvmsg \
    sysvsem \
    sysvshm \
    zip
RUN yes '' | pecl install apcu \
    igbinary \
    redis \
    xdebug-2.9.8 \
    YAML
RUN yes '' | pecl install mongodb
RUN set -ex && apt-get -y update && apt-get -y install
RUN set -ex && apt-get -y install tzdata && rm -f /etc/localtime && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && apt-get -y remove tzdata

RUN usermod -u 501 -s /bin/bash www-data
COPY docker-php-ext-mongodb.ini /usr/local/etc/php/conf.d/
COPY composer /usr/local/bin/
WORKDIR /var/www/
#RUN rmdir /var/www/html
