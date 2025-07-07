FROM php:8.1-fpm

ENV TZ=Asia/Shanghai

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libonig-dev \
        gcc g++ make autoconf libc-dev pkg-config libssl-dev \
        libpng-dev libjpeg-dev libfreetype6-dev libzip-dev zip unzip \
        libcurl4-openssl-dev \
        unixodbc-dev \
    # 安装 PHP 常用扩展
    && docker-php-ext-install mysqli pdo_mysql redis gd mbstring curl openssl sockets zip \
    # 安装 igbinary 扩展
    && pecl install igbinary \
    && docker-php-ext-enable igbinary \
    # 安装 SQL Server 驱动及扩展
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 \
    && pecl install pdo_sqlsrv sqlsrv \
    && docker-php-ext-enable pdo_sqlsrv sqlsrv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www/html