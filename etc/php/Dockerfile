FROM php:7.4.0-fpm

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y \
    vim \
    less \
    cron \
    pv \
    htop \
    g++ \
    libbz2-dev \
    libc-client-dev \
    libcurl4-gnutls-dev \
    libedit-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libkrb5-dev \
    libldap2-dev \
    libldb-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    libmemcached-dev \
    libpng-dev \
    libpq-dev \
    libsqlite3-dev \
    libssl-dev \
    libreadline-dev \
    libxslt1-dev \
    libzip-dev \
    memcached \
    wget \
    unzip \
    zlib1g-dev \
    gcc \
    make \
    autoconf \
    libc-dev \
    pkg-config \ 
    git \
    zip

RUN apt-get install -y libmcrypt-dev libonig-dev 
RUN docker-php-ext-install  \
    bcmath \
    bz2 \
    calendar \
    exif \
    gettext \
    opcache \
    pdo_pgsql \
    pgsql \
    mysqli \
    pdo_mysql \
    soap \
    sockets \
    xmlrpc \
    xsl \
    zip

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd
RUN PHP_OPENSSL=yes docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN docker-php-ext-configure intl
RUN docker-php-ext-install  intl
RUN docker-php-ext-configure ldap
RUN docker-php-ext-install ldap
RUN docker-php-ext-configure zip
RUN docker-php-ext-install zip

RUN rm -rf /tmp/pear ~/.pearrc

RUN pecl update-channels
RUN pecl channel-update pecl.php.net
RUN pecl install mcrypt-1.0.4 && docker-php-ext-enable mcrypt
RUN pecl install memcached && docker-php-ext-enable memcached
RUN pecl install redis && docker-php-ext-enable redis
RUN yes '' | pecl install imagick && docker-php-ext-enable imagick
RUN pecl install xdebug-2.9.8 && docker-php-ext-enable xdebug

RUN wget -O /usr/local/bin/phpunit https://phar.phpunit.de/phpunit-8.phar && chmod +x /usr/local/bin/phpunit

RUN apt-get update && \
    apt-get -y --no-install-recommends install git && \
    php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN docker-php-source delete
RUN apt-get remove -y g++ wget
RUN apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y
RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /tmp/* /var/tmp/*

WORKDIR /var/www/xnet