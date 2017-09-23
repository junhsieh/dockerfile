FROM php:7.1-fpm

RUN apt-get update

### Install iconv, mcrypt, gd
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

### Install pdo, mysql, zip
RUN docker-php-ext-install pdo pdo_mysql zip

### Install opcache
RUN docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache

COPY config/opcache.ini $PHP_INI_DIR/conf.d/

### Install xdebug
RUN pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug

### Copy configuration
COPY config/php.ini /usr/local/etc/php/
COPY config/php7.ini /usr/local/etc/php/conf.d/
COPY config/pdo.ini /usr/local/etc/php/conf.d/
COPY config/xdebug.ini /usr/local/etc/php/conf.d/

### for FPM
EXPOSE 9000

###
WORKDIR $PHP_INI_DIR

CMD ["php-fpm"]
