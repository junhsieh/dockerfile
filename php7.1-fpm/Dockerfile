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

### Install opcache
RUN docker-php-ext-configure opcache --enable-opcache \
		&& docker-php-ext-install opcache

COPY config/opcache.ini $PHP_INI_DIR/conf.d/

### Install xdebug
ENV PHP_XDEBUG_VERSION master

RUN apt-get -y install php-dev \
		&& git clone --branch ${PHP_XDEBUG_VERSION} https://github.com/xdebug/xdebug /tmp/php-xdebug \
		&& cd /tmp/php-xdebug \
		&& phpize \
		&& ./configure --enable-xdebug \
		&& make -j$(nproc) \
		&& make install \
		&& docker-php-ext-enable xdebug \
		&& rm -rf /tmp/php-xdebug

COPY config/xdebug.ini /usr/local/etc/php/conf.d/

