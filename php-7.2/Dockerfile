FROM php:7.2-apache

RUN apt-get update \
	&& apt-get install -y gnupg libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libicu-dev git subversion default-mysql-client \
	&& docker-php-ext-install -j$(nproc) iconv intl pdo pdo_mysql mysqli mbstring \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& pecl install mcrypt-1.0.2 \
	&& docker-php-ext-enable mcrypt

RUN curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/local/bin/composer

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp
