FROM php:7.4-fpm-alpine AS ext

RUN apk add gcc libc-dev make autoconf \
    && docker-php-ext-install pdo_mysql pcntl \
    && pecl install yaf redis apcu

FROM php:7.4-fpm-alpine

RUN apk add --no-cache tzdata

COPY --from=ext /usr/local/lib/php/extensions/no-debug-non-zts-20190902/* /usr/local/lib/php/extensions/no-debug-non-zts-20190902/
