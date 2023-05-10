#Container OS
FROM ubuntu:latest


#Update and upgrade base system"
RUN apt update && apt upgrade -y && apt dist-upgrade -y

## for apt to be noninteractive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

## preesed tzdata, update package index, upgrade packages and install needed software
RUN echo "tzdata tzdata/Areas select Europe" > /tmp/preseed.txt; \
    echo "tzdata tzdata/Zones/Europe select Berlin" >> /tmp/preseed.txt; \
    debconf-set-selections /tmp/preseed.txt && \
    apt-get update && \
    apt-get install -y tzdata

#Install PHP7, FastCGI Process Manager and PHP dependencies
RUN apt install php8.1 php8.1-fpm php8.1-gd php8.1-memcached php8.1-curl php8.1-mysql \
    php8.1-intl php-pear php8.1-imagick php8.1-imap \
    php8.1-ps php8.1-pspell php8.1-snmp php8.1-tidy php8.1-xmlrpc \
    php8.1-xsl php8.1-apcu wget -y

#Copy configuration files
COPY ./conf/www.conf /etc/php/8.1/fpm/pool.d/www.conf
COPY ./conf/docker-entrypoint /docker-entrypoint

RUN chmod +x /docker-entrypoint

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 9000

#Memory limit
CMD ["-m","512"]

#User to run php8.1-fpm master proccess
USER root

#Entrypoint
ENTRYPOINT ["/docker-entrypoint"]

