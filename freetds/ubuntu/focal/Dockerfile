# Image for spining the tdspool

FROM ubuntu:focal as base 

LABEL org.opencontainers.image.authors="me@tr3s.ma"

RUN apt update && apt install -y freetds-bin

COPY .pool.conf $HOME/
COPY .freetds.conf $HOME/

WORKDIR $HOME

CMD ["tdspool", "-c", ".pool.conf", "-l","/tmp/tdspool.log", "clientpool"]