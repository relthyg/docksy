ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /var/www

# non-root user
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

RUN groupmod -o -g ${PGID} www-data && \
    usermod -o -u ${PUID} -g www-data www-data

# locales
ARG LOCALE=POSIX
ENV LC_ALL ${LOCALE}

# essentials
RUN apt-get update && pecl channel-update pecl.php.net &&\
    apt-get install -y \
        libicu-dev \
        libzip-dev \
        libjpeg-dev \
        libpng-dev \
        apt-utils \
        git \
        vim \
        zip &&\
    docker-php-ext-install \
        intl \
        opcache \
        pdo \
        pdo_mysql \
        zip

# apcu
RUN pecl install apcu && docker-php-ext-enable apcu

# xdebug
RUN pecl install xdebug-3.0.2 && docker-php-ext-enable xdebug

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# symfony cli
RUN curl -sS https://get.symfony.com/cli/installer | bash && mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# node
RUN curl -sS https://deb.nodesource.com/setup_lts.x | bash - && apt-get install -yqq nodejs

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
