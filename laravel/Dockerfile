FROM eboraas/apache-php
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN apt-get update && apt-get -y install git curl php-json php-mbstring php-zip php-dom && apt-get -y autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN /usr/sbin/a2enmod rewrite

ADD 000-laravel.conf /etc/apache2/sites-available/
ADD 001-laravel-ssl.conf /etc/apache2/sites-available/
RUN /usr/sbin/a2dissite '*' && /usr/sbin/a2ensite 000-laravel 001-laravel-ssl

RUN /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php
RUN /bin/mv composer.phar /usr/local/bin/composer
RUN /usr/local/bin/composer create-project laravel/laravel /var/www/laravel --prefer-dist
RUN /bin/chown www-data:www-data -R /var/www/laravel/storage /var/www/laravel/bootstrap/cache

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

