FROM php:7.1-apache

RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update \
  && apt-get install -y \
    git \
    gnupg2 \
    libpng-dev \
  && apt-get autoremove -yqq --purge \
  && apt-get clean \
  && rm -Rf /var/lib/apt/lists/*
  
# MySQL v8 container uses cached_sha2 passwords, which aren't supported by
# any of the mysql clients in debian.  Use the upstream community package
# instead.
COPY mysql.gpg /tmp/mysql.gpg
RUN apt-key add /tmp/mysql.gpg \
  && apt-key adv --keyserver keys.gnupg.net --recv-keys 5072E1F5 \
  && rm /tmp/mysql.gpg
COPY mysql.list /etc/apt/sources.list.d/mysql.list

RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update \
  && apt-get install -y \
    mysql-client \
  && apt-get autoremove -yqq --purge \
  && apt-get clean \
  && rm -Rf /var/lib/apt/lists/*

RUN docker-php-ext-install gd \
  && docker-php-ext-install pdo_mysql

RUN rm -Rf /var/www/html
RUN mkdir /var/cc_docs
RUN git clone --depth 1 https://github.com/judsonmitchell/ClinicCases /var/www/html
COPY _CONFIG.php /var/www/html
COPY db.php /var/www/html
COPY php.ini /usr/local/etc/php/php.ini

RUN chown -R www-data:www-data /var/www
RUN chown -R www-data:www-data /var/cc_docs

