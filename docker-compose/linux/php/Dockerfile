FROM php:8.1-fpm

ENV TZ=Asia/Shanghai

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        gnupg \
        unixodbc \
        unixodbc-dev \
        libodbc1 \
        libonig-dev \
        gcc g++ make autoconf libc-dev pkg-config libssl-dev \
        libpng-dev libjpeg-dev libfreetype6-dev libzip-dev zip unzip \
        libcurl4-openssl-dev \
    && docker-php-ext-install pdo_mysql mysqli gd mbstring sockets curl opcache fileinfo zip

RUN pecl install igbinary redis \
    && docker-php-ext-enable igbinary redis

RUN mkdir -p /etc/apt/sources.list.d \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 \
    && pecl install pdo_sqlsrv sqlsrv \
    && docker-php-ext-enable pdo_sqlsrv sqlsrv

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www/html