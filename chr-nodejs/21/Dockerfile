FROM --platform=$TARGETOS/$TARGETARCH debian:buster-slim
FROM --platform=$TARGETOS/$TARGETARCH node:21-bullseye-slim

LABEL author="Cafirexos" maintainer="contacto@cafirexos.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -f install && apt-get -y install wget gnupg2 apt-utils
RUN apt update
RUN apt install -y wget net-tools iproute2 gnupg2 xvfb pulseaudio apt-transport-https

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=arm64] http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list.d/chromium.list \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && apt-get update \
    && apt-get install -y chromium --no-install-recommends --allow-downgrades \
           fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-kacst fonts-freefont-ttf \
           ffmpeg iproute2 git sqlite3 python3 tzdata ca-certificates dnsutils build-essential \
    && npm -g install npm@latest

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
