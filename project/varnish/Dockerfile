#Container OS
FROM ubuntu:latest

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install Varnish Cache Server
RUN apt install varnish dnsutils -y

#Copy configuration files
COPY ./conf/default.vcl /etc/varnish/

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 80

#Memory limit

#User to run Varnish master proccess
USER root

#Run Varnish proccess
CMD ["varnishd", "-F", "-a", ":80", "-T", "localhost:6082", "-f", "/etc/varnish/default.vcl", "-S", "/etc/varnish/secret", "-s", "malloc,256m", "-p", "http_resp_hdr_len=65536", "-p", "http_resp_size=98304"]
