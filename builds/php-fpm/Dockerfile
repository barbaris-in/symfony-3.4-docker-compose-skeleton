FROM php:7.1-fpm

ADD php.ini /usr/local/etc/php/conf.d/

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get update && apt-get install zip unzip wget git libmagickwand-dev imagemagick exiftool libssl-dev libicu-dev g++ -y

RUN docker-php-ext-configure exif
RUN docker-php-ext-install exif
RUN docker-php-ext-enable exif

RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

RUN yes | pecl install imagick
RUN docker-php-ext-enable imagick

RUN yes | pecl install mongodb
RUN docker-php-ext-enable mongodb

#RUN print "\n" | pecl install mongo
#RUN docker-php-ext-enable mongo

RUN yes | pecl install xdebug
ADD xdebug.ini /usr/local/etc/php/conf.d/

RUN docker-php-ext-install intl

RUN docker-php-ext-install sockets

RUN docker-php-ext-install zip

RUN echo 'alias ll="ls -alF"' >> ~/.bashrc
RUN echo 'alias la="ls -A"' >> ~/.bashrc
RUN echo 'alias  l="ls -CF"' >> ~/.bashrc

RUN echo 'alias  dsu="php bin/console doctrine:schema:update --dump-sql --force"' >> ~/.bashrc
RUN echo 'alias  dge="php bin/console doctrine:generate:entity"' >> ~/.bashrc
RUN echo 'alias  dfl="php bin/console doctrine:schema:drop --force && php bin/console doctrine:schema:create && php bin/console doctrine:fixtures:load"' >> ~/.bashrc
RUN echo 'alias  gb="php bin/console generate:bundle"' >> ~/.bashrc
RUN echo 'alias  dr="php bin/console debug:router"' >> ~/.bashrc
RUN echo 'alias  ai="php bin/console asset:install --symlink --relative"' >> ~/.bashrc
RUN echo 'alias  ad="php bin/console assetic:dump"' >> ~/.bashrc
RUN echo 'alias  trans="php bin/console translation:extract en fr --config=cocorico"' >> ~/.bashrc
RUN echo 'alias  cc="rm -fr /app/var/cache/* && chmod -R 777 /app/var/cache /app/var/logs /app/var/sessions"' >> ~/.bashrc
RUN echo 'alias  ccc="php /app/bin/console cache:clear && chmod -R 777 /app/var/cache /app/var/logs /app/var/sessions"' >> ~/.bashrc

ENV COMPOSER_ALLOW_SUPERUSER=1

WORKDIR /app