FROM php:7.0-fpm-alpine


ENV COMPOSER_HOME=/usr/local/composer \
    PATH=/usr/local/composer/vendor/bin:$PATH

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
COPY fpm/etc/supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN apk --no-cache update && \
    apk upgrade && \
    apk --no-cache add \
    supervisor \
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
# Ext
    && chmod 775 /usr/local/bin/install-php-extensions \
    && install-php-extensions gd zip mysqli zip intl sodium

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini && \
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 128M/g' /usr/local/etc/php/php.ini && \
    sed -i 's/post_max_size = 8M/post_max_size = 128M/g' /usr/local/etc/php/php.ini

RUN sed -i 's/9000/9070/g' /usr/local/etc/php-fpm.d/www.conf
RUN sed -i 's/9000/9070/g' /usr/local/etc/php-fpm.d/zz-docker.conf

# # Ext
# RUN apt-get update -y \
#     && apt-get install libsodium-dev -y \
#     && install-php-extensions gd zip mysqli zip intl sodium

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]