#Container OS
FROM ubuntu:latest

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install Apache Web Server and PHP dependencies
RUN apt install apache2 wget dnsutils -y

#Copy configuration files
COPY ./conf/drupal.conf /etc/apache2/sites-available/
COPY ./conf/docker-entrypoint /docker-entrypoint

#Setup web server
RUN a2enmod rewrite actions alias proxy_fcgi && a2dissite 000-default && a2ensite drupal

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 8080

#Memory limit
CMD ["-m","512"]

#User to run apache master proccess
USER root

#Entrypoint configuration
RUN chmod +x /docker-entrypoint
ENTRYPOINT ["/docker-entrypoint"]
