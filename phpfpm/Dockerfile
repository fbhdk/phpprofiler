FROM php:8-fpm

RUN apt -yqq update && apt install -y zlib1g-dev libicu-dev g++ 

RUN pecl install -f xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install intl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql
