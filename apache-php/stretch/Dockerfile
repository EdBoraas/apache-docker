FROM eboraas/apache:stretch
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN apt-get update && apt-get -y install php php-mysql && apt-get clean && rm -r /var/lib/apt/lists/*
RUN /usr/sbin/a2dismod 'mpm_*' && /usr/sbin/a2enmod mpm_prefork

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

