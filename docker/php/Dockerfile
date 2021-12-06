ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm-alpine

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /srv/app

# non-root user
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

RUN addgroup -g ${PGID} docksy && \
  adduser -G docksy -u ${PUID} --disabled-password docksy

# locales
ARG LOCALE=POSIX
ENV LC_ALL ${LOCALE}

RUN apk add --no-cache \
		acl \
		fcgi \
		file \
		gettext \
		git \
		gnu-libiconv \
        imagemagick \
        vim \
        zip

RUN apk add --update --no-cache --virtual .build-dependencies \
            $PHPIZE_DEPS \
            icu-dev \
            libzip-dev \
            zlib-dev \
            imagemagick-dev \
            jpeg-dev \
            libpng-dev \
        && pecl install \
              apcu \
              opcache \
              xdebug-3.1.2 \
              imagick \
        && docker-php-ext-enable \
              apcu \
              xdebug \
              imagick \
        && pecl clear-cache \
        && apk del .build-dependencies

# node
ENV ALPINE_MIRROR "http://dl-cdn.alpinelinux.org/alpine"
RUN echo "${ALPINE_MIRROR}/edge/main" >> /etc/apk/repositories && \
    apk add --no-cache nodejs-current  --repository="http://dl-cdn.alpinelinux.org/alpine/edge/community"

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=symfonycorp/cli /symfony /usr/bin/symfony
COPY --from=oskarstark/php-cs-fixer-ga /usr/local/bin/php-cs-fixer /usr/bin/php-cs-fixer

