FROM eboraas/apache-php
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN apt-get update && apt-get -y install git php5-dev libpcre3-dev gcc make && apt-get -y autoremove && apt-get clean

RUN /usr/sbin/a2enmod rewrite
# Note: "default" is enabled in the default installation, and "default-ssl" is enabled in the eboraas/apache image, so no need to recreate the symlinks here, just copy the new site definitions into place
ADD default /etc/apache2/sites-available/
ADD default-ssl /etc/apache2/sites-available/

WORKDIR /tmp
RUN /usr/bin/git clone git://github.com/phalcon/cphalcon.git
WORKDIR /tmp/cphalcon/build
RUN ./install
RUN /bin/echo 'extension=phalcon.so' >/etc/php5/mods-available/phalcon.ini
RUN /usr/sbin/php5enmod phalcon
RUN /bin/rm -rf /tmp/cphalcon/
WORKDIR /var/www/phalcon/public
RUN /bin/mv /var/www/index.html /var/www/phalcon/public

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

