FROM php:8.1-fpm

LABEL com.skywire.container="Php-Fpm"
LABEL version="0.0.1"
LABEL description="PHP-FPM 8.1 Docker Container"

ENV	HOME /root
ENV	GOPATH $HOME/go
WORKDIR /$HOME

RUN apt-get update && apt-get install -y \
            default-mysql-client \
            golang-go \
            git \
            npm \
            libfreetype6-dev \
            libjpeg62-turbo-dev \
            libpng-dev \
            libxml2-dev \
            libmcrypt-dev \
            libxslt-dev \
            libzip-dev \
            vim \
            redis-tools \
            pv \
            zsh \
            wget \
            wkhtmltopdf \
        && docker-php-ext-configure gd --with-freetype --with-jpeg \
        && docker-php-ext-install -j$(nproc) gd \
        && pecl install xdebug-3.1.4 \
        && docker-php-ext-install pdo_mysql soap intl bcmath xsl zip sockets \
        && docker-php-ext-enable opcache xdebug

COPY src/php.ini $PHP_INI_DIR/
COPY src/conf.d/xdebug.ini $PHP_INI_DIR/xdebug.ini

#Install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

#install ZSH
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

WORKDIR /var/www/html
