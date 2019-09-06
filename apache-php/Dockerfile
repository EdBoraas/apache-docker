FROM eboraas/apache
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN apt-get update && apt-get -y install php php-mysql php-fpm && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN /usr/sbin/a2enmod proxy_fcgi setenvif && /usr/sbin/a2enconf php7.3-fpm

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

