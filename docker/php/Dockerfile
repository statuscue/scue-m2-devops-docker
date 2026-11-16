FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
    git unzip libicu-dev libxml2-dev libxslt-dev libzip-dev libonig-dev \
    libpng-dev libjpeg-dev libfreetype6-dev zlib1g-dev libssl-dev \
    libssh-dev openssh-client mariadb-client \
    && docker-php-ext-install \
        intl xsl zip pdo_mysql soap sockets bcmath opcache \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

RUN mkdir -p /root/.ssh && ssh-keyscan github.com >> /root/.ssh/known_hosts

ARG GITHUB_TOKEN
ARG AMASTY_USERNAME
ARG AMASTY_PASSWORD
ARG MAGENTO_USERNAME
ARG MAGENTO_PASSWORD

RUN composer config --global github-oauth.github.com ${GITHUB_TOKEN}
RUN composer config --global http-basic.composer.amasty.com ${AMASTY_USERNAME} ${AMASTY_PASSWORD}
RUN composer config --global http-basic.repo.magento.com ${MAGENTO_USERNAME} ${MAGENTO_PASSWORD}

WORKDIR /var/www/html

