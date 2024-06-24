FROM php:7.3-apache-stretch

ENV APP_ENV=dev
ENV APP_DEBUG=true
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN echo 'deb http://archive.debian.org/debian/ stretch main non-free contrib\ndeb-src http://archive.debian.org/debian/ stretch main non-free contrib\ndeb http://archive.debian.org/debian-security/ stretch/updates main non-free contrib\ndeb-src http://archive.debian.org/debian-security/ stretch/updates main non-free contrib' > /etc/apt/sources.list
RUN apt-get update && apt-get install -y zip libpng-dev libzip-dev git vim
RUN docker-php-ext-install pdo pdo_mysql gd zip
RUN git config --global user.email "andradewall0@gmail.com" && \
    git config --global user.name "Wallace Andrade" && \
    git config --global init.defaultBranch main

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini && \
    sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /usr/local/etc/php/php.ini && \
    sed -i 's/set_time_limit = 30/set_time_limit = 60/g' /usr/local/etc/php/php.ini && \
    sed -i 's/max_execution_time = 30/max_execution_time = 60/g' /usr/local/etc/php/php.ini 

COPY code /var/www/html/
COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

COPY docker/apache/000-default.conf /etc/apache2/sites-available/000-default.conf

RUN a2enmod rewrite
