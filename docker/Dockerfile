FROM php:8.4-fpm

ARG USER_ID=1000
ARG GROUP_ID=1000

WORKDIR /var/www/ida-dev

RUN set -exv; \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    libzip-dev \
    libicu-dev \
    libcurl4-openssl-dev

RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash -E
RUN apt install -y symfony-cli

RUN docker-php-ext-install opcache \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install curl

RUN set -exv; \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --version=2.8.6 --filename=composer

RUN apt install -y mc

RUN git config --global user.email "after@ya.ru"
RUN git config --global user.name "Maxim Gabidullin"
RUN git config --global --add safe.directory /var/www/ida-dev

CMD ["php-fpm"]
