FROM eboraas/apache-php
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN /usr/sbin/a2enmod rewrite

ADD 000-phalcon.conf /etc/apache2/sites-available/
ADD 001-phalcon-ssl.conf /etc/apache2/sites-available/
RUN /usr/sbin/a2dissite '*' && /usr/sbin/a2ensite 000-phalcon 001-phalcon-ssl

WORKDIR /tmp
# Run build process on one line to avoid generating bloat via intermediate images
RUN /usr/bin/apt-get update && apt-get -y install git php-dev libpcre3-dev gcc make && \
    /usr/bin/git clone git://github.com/phalcon/cphalcon.git && \
    cd cphalcon/build/ && \
    ./install && \
    cd /tmp && \
    /bin/rm -rf /tmp/cphalcon/ && \
    /usr/bin/apt-get -y purge git php-dev libpcre3-dev gcc make && apt-get -y autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN /bin/echo 'extension=phalcon.so' > /etc/php/7.3/mods-available/phalcon.ini
RUN /usr/sbin/phpenmod phalcon
WORKDIR /var/www/phalcon/public
RUN /bin/echo '<html><body><h1>It works!</h1></body></html>' > /var/www/phalcon/public/index.html

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

