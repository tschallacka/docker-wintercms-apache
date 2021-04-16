FROM ubuntu:18.04

MAINTAINER echo <tschallacka@outlook.com>

ENV XDEBUG_PORT 9000

# Install System Dependencies
RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive  apt-get install -y --no-install-recommends \
	software-properties-common \
	&& add-apt-repository ppa:ondrej/php \
	&& apt-get update \
	&& DEBIAN_FRONTEND=noninteractive  apt-get install -y \
	sudo \
	php7.4 \
	php7.4-opcache \
  	php7.4-bcmath \
  	php7.4-gd \
  	php7.4-intl \
  	php7.4-mysql \
  	php7.4-soap \
  	php7.4-xsl \
  	php7.4-zip \
  	php7.4-sockets \
  	php7.4-ctype \
  	php7.4-curl \
  	php7.4-dom \
  	php7.4-fileinfo \
  	php7.4-gd \
  	php7.4-redis \
  	php7.4-xml \
  	php7.4-mbstring \
  	php7.4-zip \
  	php7.4-oauth \
  	php7.4-xdebug \
  	apache2 \
	libicu-dev \
	openssl \
	apt-utils \
	gnupg \
	redis-tools \
	mariadb-client \
	git \
	mc \
	nano \
	vim \
	wget \
	curl \
	lynx \
	psmisc \
	unzip \
	tar \
	cron \
	nano \
	bash-completion \
	&& apt-get clean


# Install Node, NVM, NPM and Grunt

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  	&& apt-get install -y nodejs build-essential \
    && npm i -g grunt-cli yarn

# Install Composer

RUN	curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

ENV PATH="/var/www/.composer/vendor/bin/:${PATH}"

# Configuring system

ADD /.docker/config/php.ini /usr/local/etc/php/php.ini
ADD /.docker/config/wintercms.conf /etc/apache2/sites-available/wintercms.conf
ADD /.docker/config/custom-xdebug.ini /usr/local/etc/php/conf.d/custom-xdebug.ini
COPY /.docker/bin/* /usr/local/bin/
COPY /.docker/users/* /var/www/
RUN chmod +x /usr/local/bin/*
RUN ln -s /etc/apache2/sites-available/wintercms.conf /etc/apache2/sites-enabled/wintercms.conf

RUN chmod 777 -Rf /var/www /var/www/.* \
	&& chown -Rf www-data:www-data /var/www /var/www/.* \
	&& usermod -u 1000 www-data \
	&& chsh -s /bin/bash www-data\
	&& a2enmod rewrite \
	&& a2enmod headers

VOLUME /var/www/html
WORKDIR /var/www/html
