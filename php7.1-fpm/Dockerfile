FROM php:7.1-fpm

RUN apt-get update

### Install iconv
RUN apt-get -y install \
		&& docker-php-ext-install -j$(nproc) iconv

### Install mcrypt
RUN apt-get -y install libmcrypt-dev \
		&& docker-php-ext-install -j$(nproc) mcrypt

### Install gd
RUN apt-get -y install libfreetype6-dev libjpeg62-turbo-dev libpng12-dev \
		&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
		&& docker-php-ext-install -j$(nproc) gd
