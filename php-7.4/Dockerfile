FROM php:7.4-apache

# WordPress Stuff
RUN apt-get update \
	&& apt-get install -y gnupg libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libicu-dev libonig-dev git subversion default-mysql-client \
	&& docker-php-ext-install -j$(nproc) iconv intl pdo pdo_mysql mysqli mbstring \
	&& docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& pecl install mcrypt-1.0.3 \
	&& docker-php-ext-enable mcrypt

# Puppeteer Compatibility
RUN apt-get install -y \
    gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 \
    libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 \
    libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget libgbm-dev

# Composer
RUN curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/local/bin/composer \
	&& apt-get install -y \
        zlib1g-dev \
        libzip-dev \
        unzip \
    && docker-php-ext-install zip

# WP CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp
