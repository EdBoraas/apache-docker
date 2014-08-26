FROM eboraas/apache-php:sid
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN apt-get update && apt-get -y install git curl php5-mcrypt php5-json && apt-get -y autoremove && apt-get clean

RUN /usr/sbin/a2enmod rewrite
ADD default /etc/apache2/sites-available/
ADD default-ssl /etc/apache2/sites-available/

RUN /usr/bin/curl -sS https://getcomposer.org/installer |/usr/bin/php
RUN /bin/mv composer.phar /usr/local/bin/composer
RUN /usr/local/bin/composer create-project laravel/laravel /var/www/laravel --prefer-dist
RUN /bin/chown www-data:www-data -R /var/www/laravel/app/storage

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

