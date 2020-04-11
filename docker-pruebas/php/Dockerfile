ARG PHP_VERSION=""
FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine

# Install dependencies
RUN apk --no-cache --update add \
    gcc \
    autoconf \
    make \
    libxml2-dev \
    sqlite-dev \
    curl-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    icu-libs \
    icu-dev \
    zlib \
    zlib-dev \
    libc-dev \
    freetype-dev && \
    pecl install apcu \
    xdebug && \
    docker-php-ext-enable apcu  \
    xdebug && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*

# Configure PHP extensions
RUN docker-php-ext-configure json && \
    docker-php-ext-configure session && \
    docker-php-ext-configure ctype && \
    docker-php-ext-configure tokenizer && \
    docker-php-ext-configure simplexml && \
    docker-php-ext-configure dom && \
    docker-php-ext-configure mbstring && \
    docker-php-ext-configure zip && \
    docker-php-ext-configure pdo && \
    docker-php-ext-configure pdo_sqlite && \
    docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure curl && \
    docker-php-ext-configure iconv && \
    docker-php-ext-configure xml && \
    docker-php-ext-configure phar && \
    docker-php-ext-configure intl && \
    docker-php-ext-configure opcache --enable-opcache && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Build and install PHP extensions
RUN docker-php-ext-install json \
    session \
    ctype \
    tokenizer \
    simplexml \
    dom \
    mbstring \
    zip \
    pdo \
    pdo_sqlite \
    pdo_mysql \
    curl \
    iconv \
    xml  \
    phar \
    intl \
    opcache \
    gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer