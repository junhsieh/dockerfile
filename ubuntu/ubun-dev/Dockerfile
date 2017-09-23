###
### docker build -t junhsieh/ubun-dev:1.0 -f Dockerfile .
###
FROM ubuntu:16.04

RUN apt-get update 

### Install Git
RUN apt-get -y install dh-autoreconf libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev curl \
&& cd /usr/local/src/ \
&& curl -L https://github.com/git/git/archive/v2.13.5.tar.gz -o git.tar.gz \
&& tar zxvf git.tar.gz \
&& cd git-2.13.5/ \
&& make configure \
&& ./configure --prefix=/usr \
&& make all \
&& make install

### Install Vim
RUN apt-get -y install libncurses5-dev python-dev ruby-dev libperl-dev ruby-dev liblua5.3-dev exuberant-ctags cscope \
&& ln -s /usr/include/lua5.3 /usr/include/lua \
&& ln -s /usr/lib/x86_64-linux-gnu/liblua5.3.so /usr/local/lib/liblua.so \
&& cd /usr/local/src \
&& git clone https://github.com/vim/vim.git \
&& cd vim \
&& ./configure --prefix=/usr --with-features=huge --enable-multibyte --enable-pythoninterp --enable-rubyinterp --enable-perlinterp --enable-luainterp --enable-cscope \
&& make \
&& make install

### Install Go
RUN curl 'https://storage.googleapis.com/golang/go1.9.linux-amd64.tar.gz' -o go.tar.gz \
&& tar -zxvf go.tar.gz -C /usr/local \
&& rm -f go.tar.gz

### Install tmux
RUN apt-get -y install tmux

### Install some utilities
RUN apt-get -y install wget curl less tree net-tools iproute software-properties-common

### Set up the environmental configuration
RUN cd \
&& git clone https://github.com/junhsieh/config_centos_v2.git \
&& bash config_centos_v2/script/setHomeConfig.sh \
&& cd / \
&& ln -s usr/local/apache2/htdocs www

### Install PHP 7.1
RUN locale-gen en_US.UTF-8 \
&& export LANG=en_US.UTF-8 \
&& add-apt-repository ppa:ondrej/php \
&& apt-get update \
&& apt-get -y install php7.1 php7.1-common php7.1-mbstring php7.1-xml php7.1-curl php7.1-mysql php7.1-gd php7.1-redis

### Install MySQL client
RUN apt-get -y install mysql-client

### Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
&& php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
&& php composer-setup.php \
&& php -r "unlink('composer-setup.php');" \
&& mv composer.phar /usr/local/bin/composer \
&& chmod 755 /usr/local/bin/composer

### Install Drupal Console
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
&& mv drupal.phar /usr/local/bin/drupal \
&& chmod 755 /usr/local/bin/drupal

#RUN composer require drupal/console:~1.0 \
#--prefer-dist \
#--optimize-autoloader

### for xdebug
EXPOSE 9009

###
WORKDIR /www

