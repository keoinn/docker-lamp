# THIS IS AN AUTOGENERATED FILE. DO NOT EDIT THIS FILE DIRECTLY
# Content of this file is based on Dockerfile.template-debian

FROM php:7.4-fpm-alpine

ENV COMPOSER_HOME=/usr/local/composer \
    PATH=/usr/local/composer/vendor/bin:$PATH

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
COPY fpm/etc/supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN apk --no-cache update && \
    apk upgrade && \
    apk --no-cache add \
    supervisor \
    openssl \
# Composer dependencies:
    openssl \
    zip \
    unzip \
    curl \
    wget \
    git \
    mercurial \
    subversion \
    zlib-dev \
    libpng-dev \
    libzip-dev \
    icu-dev \
# Composer
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod 755 /usr/local/bin/composer \
    && chown www-data:www-data $COMPOSER_HOME \
    && chown www-data:www-data $COMPOSER_HOME -R \
    && chmod 775 $COMPOSER_HOME \
    && chmod 775 $COMPOSER_HOME -R \
    && chmod 775 /usr/local/bin/install-php-extensions \
# Ext
    && chmod 775 /usr/local/bin/install-php-extensions \
    && install-php-extensions gd zip mysqli zip intl sodium

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini && \
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 1024/g' /usr/local/etc/php/php.ini && \
    sed -i 's/post_max_size = 8M/post_max_size = 1024/g' /usr/local/etc/php/php.ini

RUN sed -i 's/9000/9074/g' /usr/local/etc/php-fpm.d/www.conf
RUN sed -i 's/9000/9074/g' /usr/local/etc/php-fpm.d/zz-docker.conf

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

