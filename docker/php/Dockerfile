ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /srv/app

ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

ARG LOCALE=POSIX
ENV LC_ALL ${LOCALE}

RUN addgroup -g ${PGID} docksy && \
  adduser -G docksy -u ${PUID} --disabled-password docksy

RUN apk add --no-cache \
    acl \
    bash \
    fcgi \
    file \
    gettext \
    git \
    gnu-libiconv \
    nodejs-current \
    npm \
    vim \
    zip \
    $PHPIZE_DEPS \
    icu-dev \
    libzip-dev \
    zlib-dev \
    && \
    npm i -g corepack

ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN install-php-extensions \
    intl \
    zip \
    pdo \
    pdo_mysql \
    apcu \
    xdebug

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=oskarstark/php-cs-fixer-ga /usr/local/bin/php-cs-fixer /usr/bin/php-cs-fixer
RUN curl -sS https://get.symfony.com/cli/installer | bash && mv $HOME/.symfony5/bin/symfony /usr/bin/symfony
