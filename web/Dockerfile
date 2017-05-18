FROM php:5.5-apache

RUN apt-get update --fix-missing
#RUN apt-get install php5-mysql
RUN apt-get install -y vim \
    mysql-client \
    sudo \
    nodejs \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    apt-utils \
    libjpeg-dev \
    libpng12-0 \
    libpng12-dev \
    libfreetype6 \
    libfreetype6-dev \
    ttf-dejavu \
    php5-gd

RUN docker-php-ext-install mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install calendar \
    && pecl install mailparse-2.1.6 \
    && pear install Mail \
    && pear install Mail_Mime \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \ 
    && docker-php-ext-install -j$(nproc) gd

RUN adduser --disabled-password --gecos '' developer
RUN adduser developer sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

COPY wordpress /var/www/html/hasan
COPY phpmyadmin /var/www/html/phpmyadmin


RUN chown -R developer:developer /var/www/html
WORKDIR /var/www/html/
#WORKDIR /var/www/html/wp-content/plugins
RUN chown -R www-data:www-data /var/www/html
RUN touch /var/log/php5.log && chown www-data:www-data /var/log/php5.log
