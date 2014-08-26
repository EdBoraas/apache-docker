FROM eboraas/apache-php:stable
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN /usr/sbin/a2enmod rewrite

# This is no longer available by default in jessie's apache2
RUN /usr/sbin/a2enmod socache_shmcb || true

# Note: "default" is enabled in the default installation, and "default-ssl" is enabled in the eboraas/apache image, so no need to recreate the symlinks here, just copy the new site definitions into place
ADD default /etc/apache2/sites-available/
ADD default-ssl /etc/apache2/sites-available/

WORKDIR /tmp
# Run build process on one line to avoid generating bloat via intermediate images
RUN /usr/bin/apt-get update && apt-get -y install git php5-dev libpcre3-dev gcc make && \
    /usr/bin/git clone git://github.com/phalcon/cphalcon.git && \
    cd cphalcon/build/ && \
    ./install && \
    cd /tmp && \
    /bin/rm -rf /tmp/cphalcon/ && \
    /usr/bin/apt-get -y purge git php5-dev libpcre3-dev gcc make && apt-get -y autoremove && apt-get clean
RUN /bin/echo 'extension=phalcon.so' >/etc/php5/mods-available/phalcon.ini
RUN /usr/sbin/php5enmod phalcon
WORKDIR /var/www/phalcon/public
RUN /bin/echo '<html><body><h1>It works!</h1></body></html>' > /var/www/phalcon/public/index.html

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

