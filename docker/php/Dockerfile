FROM php:7.4-fpm-alpine

LABEL maintainer="KULDIP PIPALIYA <kuldipem@gmail.com>"

RUN apk add --update \
    icu-dev \
    icu \
    make \
    curl \
    nodejs \
    yarn

RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN docker-php-ext-install -j$(nproc) intl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

RUN curl -LO https://github.com/symfony/cli/releases/download/v4.19.0/symfony_linux_amd64.gz
RUN gunzip symfony_linux_amd64.gz
RUN chmod +x symfony_linux_amd64
RUN mv symfony_linux_amd64 /usr/local/bin/symfony

ADD php.ini /etc/php/conf.d/
ADD php.ini /etc/php/cli/conf.d/
ADD php-fpm.conf /etc/php/php-fpm.d/
#ADD xdebug.ini  /etc/php/conf.d/

WORKDIR /var/www/symfony

EXPOSE 9000

CMD ["php-fpm", "-F"]
