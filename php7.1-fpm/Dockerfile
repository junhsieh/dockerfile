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
		php71u-soap \
		php71u-process \
		php71u-fpm-httpd

EXPOSE 9000

CMD ["php-fpm", "-F"]

### Running php-fpm in Docker based on CentOS.
### Some important settings to be changed:
### 
### # vim /etc/php-fpm.d/www.conf
### 
### user = php-fpm
### group = php-fpm
### 
### ; Note: Ubuntu uses www-data user. Add php-fpm user to www-data group if the other container uses it
### ; # groupadd -g 33 www-data
### ; # useradd www-data -m -c 'web user' -u 33 -g 33
### ; # usermod -a -G www-data php-fpm
### ; # id php-fpm
### ; Now, restart this container to ensure php-fpm user is in www-data group.
### 
### listen = 9000
### 
### ; Comment out the following line:
### ;listen.allowed_clients = 127.0.0.1
### 
### ; Note: "listen.allowed_clients = any" will not work.
### ; Note: "listen.allowed_clients = other-container-name" will not work.
### 
### ; Uncomment the following line to debug the issue:
### catch_workers_output = yes
