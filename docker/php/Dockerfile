FROM php:7.4-cli

RUN echo "Asia/Tokyo" > /etc/timezone

RUN apt-get update && apt-get install -y \
    gnupg \
    lsb-release \
    libpng-dev \
    libxslt-dev \
    zlib1g-dev \
    libzip-dev \
    libpq-dev \
    librabbitmq-dev \
    zip \
    unzip \
    docker \
    docker-compose \
    npm \
    git

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
    && cat /etc/apt/sources.list.d/pgdg.list \
    && curl --silent https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
    && apt-get update \
    && apt-get install --no-install-recommends -y  \
        postgresql-client-13 \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis

RUN docker-php-ext-install \
    pdo_pgsql zip gd xsl \
    redis \
    intl

# Installing amqp docker-php-ext-install cannot install ampq
RUN pecl install amqp
RUN docker-php-ext-enable amqp

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Installing yarn
RUN npm install --global yarn

# Setup php.ini 
RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

# Installing composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm -rf composer-setup.php

# Installing symfony
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

