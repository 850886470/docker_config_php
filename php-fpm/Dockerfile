FROM php:7.2-fpm
COPY ./upload.ini /usr/local/etc/php/conf.d/upload.ini
COPY ./source.list /etc/apt/sources.list
COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN apt-get update && apt-get install -y --no-install-recommends git zlib1g-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install pdo pdo_mysql \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
RUN curl -o /usr/local/bin/composer https://getcomposer.org/download/1.8.6/composer.phar  \
    && chmod a+x /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org \
    &&  pecl install xdebug-2.7.0beta1 \
    && docker-php-ext-enable xdebug
