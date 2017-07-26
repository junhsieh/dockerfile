FROM centos:centos7

RUN curl 'https://setup.ius.io/' -o setup-ius.sh \
	&& bash setup-ius.sh \
	&& rm -f setup-ius.sh \
	&& yum -y update \
	&& yum -y install \
		php71u-common \
		php71u-cli \
		php71u-fpm \
		php71u-opcache \
		php71u-xml \
		php71u-json \
		php71u-pdo \
		php71u-mysqlnd \
		php71u-intl \
		php71u-mbstring \
		php71u-mcrypt \
		php71u-gd \
		php71u-process \
		php71u-fpm-httpd

EXPOSE 9000
CMD ["php-fpm"]
