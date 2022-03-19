FROM ubuntu:focal

RUN apt-get update && apt-get install -y stunnel4 && apt-get clean
COPY stunnel.conf /etc/stunnel/stunnel.conf

CMD [ "stunnel" ]