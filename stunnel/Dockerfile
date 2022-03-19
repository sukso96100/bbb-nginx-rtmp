FROM ubuntu:focal
LABEL org.opencontainers.image.source https://github.com/sukso96100/bbb-nginx-rtmp

RUN apt-get update \
    && apt-get install -y stunnel4 ca-certificates \
    && apt-get clean \
    && mkdir -p /etc/stunnel/conf.d/
COPY stunnel.conf /etc/stunnel/stunnel.conf
COPY conf.d/ /etc/stunnel/conf.d/
ENTRYPOINT [ "/usr/bin/stunnel" ]