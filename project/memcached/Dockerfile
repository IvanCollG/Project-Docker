#Container OS
FROM debian:stretch

#Update and upgrade base system
RUN apt update && apt upgrade -y && apt dist-upgrade -y

#Install MemCached
RUN apt install memcached -y

#Cleaning container
RUN apt-get clean && \
    apt-get autoclean && \
    apt-get autoremove -y && \
    rm -rf /build && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*

#Port to expose
EXPOSE 11211

#Memory limit
CMD ["-m","256"]

#User to run apache master proccess
USER daemon

#Run MemCached Proccess
ENTRYPOINT memcached

