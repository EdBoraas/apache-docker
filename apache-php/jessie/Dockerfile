FROM eboraas/apache:jessie
MAINTAINER Ed Boraas <ed@boraas.ca>

RUN apt-get update && apt-get -y install php5 php5-mysql libapache2-mod-php5 && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN /usr/sbin/a2enmod mpm_prefork

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

