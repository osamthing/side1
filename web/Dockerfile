FROM php:7.3-apache

COPY ./php.ini /usr/local/etc/php/

RUN set -ex apk --no-cache add postgresql-dev libpq-dev && \
    apt-get update && apt-get install -y libpq-dev \
    vim \
    less \
    && docker-php-ext-install pdo pdo_pgsql pgsql mbstring