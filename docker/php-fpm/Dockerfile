FROM php:8.1-fpm-alpine
LABEL maintainer="Sascha Greuel <sascha@softcreatr.de>"

RUN set -eux; \
    apk add --no-cache \
        bash=~5.1.16 \
        curl=~7.83.1 \
        libxml2-dev=~2.9.14 \
        tar=~1.34 \
        imagemagick=~7 \
;

# Configure & Install PHP extensions
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN set -eux; \
    chmod +x /usr/local/bin/install-php-extensions && IPE_GD_WITHOUTAVIF=1 install-php-extensions \
        exif \
        intl \
        gd \
        gmp \
        imagick \
        pdo_mysql \
        redis \
;

# Setup entrypoint and start
COPY ./start-container.sh /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

ENTRYPOINT ["start-container", "/wsc", "5.5"]
