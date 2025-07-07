FROM php:8.1-fpm

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libonig-dev \
        gcc g++ make autoconf libc-dev pkg-config libssl-dev \
        libpng-dev libjpeg-dev libfreetype6-dev libzip-dev zip unzip \
    && docker-php-ext-install pdo_mysql mysqli gd mbstring sockets curl opcache fileinfo \
    && pecl install igbinary redis \
    && docker-php-ext-enable igbinary redis \
    # SQL Server 驱动及扩展
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/$(lsb_release -rs)/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 \
    && pecl install pdo_sqlsrv sqlsrv \
    && docker-php-ext-enable pdo_sqlsrv sqlsrv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www/html