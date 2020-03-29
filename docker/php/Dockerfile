FROM php:7.4-fpm

RUN apt-get update \
    && apt-get install -y --no-install-recommends\
        zlib1g-dev \
        libicu-dev \
        g++ \
        default-mysql-client \
        default-libmysqlclient-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libzip-dev \
        curl \
        unzip \
        libonig-dev \
        git


RUN pecl install redis-3.1.3
RUN docker-php-ext-enable redis


RUN pecl install mcrypt-1.0.3
RUN docker-php-ext-enable mcrypt


RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp
RUN docker-php-ext-install -j$(nproc) gd


RUN docker-php-ext-configure xml

RUN docker-php-ext-install mbstring iconv pdo pdo_mysql intl xml xmlrpc soap opcache zip pcntl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require --prefer-dist "hirak/prestissimo" \
    && composer global require --prefer-dist "fxp/composer-asset-plugin"
