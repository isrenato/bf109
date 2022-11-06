FROM php:8.1-fpm-alpine

ARG IS_LDE=1

# Install pcov for fast code coverage generation
RUN if [ $IS_LDE = 0 ]; then \
    apk add --no-cache --virtual .build-deps autoconf file g++ gcc libc-dev pkgconf make \
    && pecl install pcov && docker-php-ext-enable pcov \
    && apk del .build-deps; \
    fi

# Install and enable XDebug extension
RUN if [ $IS_LDE = 1 ]; then \
    apk add --no-cache --virtual .build-deps autoconf $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && apk del .build-deps; \
    fi

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

COPY . /app

WORKDIR /app
