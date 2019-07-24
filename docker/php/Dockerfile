FROM php:7.2-fpm

MAINTAINER Anton Kazarinov <askazarinov@gmail.com>

ENV COMPOSER_ALLOW_SUPERUSER 1

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
        git \
        unzip \
        zlib1g-dev \
        libcurl3-dev && \
    pecl install xdebug && \
    docker-php-ext-install \
        zip \
        curl \
        pdo_mysql && \
    docker-php-ext-enable \
        xdebug && \
    apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Download and install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Custom params for php
COPY conf.d/ /usr/local/etc/php/conf.d/

WORKDIR /app
