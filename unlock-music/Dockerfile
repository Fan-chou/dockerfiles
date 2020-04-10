FROM alpine:3
MAINTAINER JackChou <dvfanzrfo@gmail.com>

WORKDIR /root

RUN set -ex \
        && apk add --no-cache npm git nodejs caddy \
        && mkdir -p /root/unlock-music \
        && cd /root/unlock-music \
        && git clone --depth=1 https://github.com/ix64/unlock-music.git . \
        && git submodule update --init --recursive \
        && npm install \
        && npm run build \
        && mv -f /root/unlock-music/dist /root/ \
        && cd /root \
        && rm -rf /root/unlock-music \
        && apk del git \
        && echo "Asia/Shanghai" > /etc/timezone

COPY Caddyfile /etc/Caddyfile

ENV TZ=Asia/Shanghai

CMD caddy -quic --conf /etc/Caddyfile
