FROM php:8.4-fpm-alpine

RUN apk add --no-cache curl \
    wget \
    libzip-dev \
    postgresql-dev \
    icu-dev \
    rabbitmq-c-dev \
    bash \
    git \
    autoconf \
    linux-headers \
    g++ \
    make \
    mc \
    zip

RUN docker-php-ext-install bcmath sockets zip intl pdo pdo_pgsql

RUN pecl install xdebug amqp redis && docker-php-ext-enable xdebug amqp redis

RUN mkdir -p /var/log \
	&& mkdir -p /var/www/html/var \
	&& mkdir -p /var/www/html/public \
    && touch /var/log/xdebug.log \
    && chmod 777 /var/log/xdebug.log 

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/app

RUN addgroup -g 1000 www \
    && adduser -u 1000 -G www -s /bin/sh -D www

RUN chown www:www /var/app

USER www

EXPOSE 9000

CMD ["php-fpm"]
