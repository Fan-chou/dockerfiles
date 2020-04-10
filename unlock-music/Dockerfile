FROM alpine:3
MAINTAINER JackChou <dvfanzrfo@gmail.com>

WORKDIR /root

RUN set -ex \
        && apk add --no-cache npm git nodejs caddy wget\
        && mkdir -p /root/unlock-music \
        && cd /root/unlock-music \
        && git clone --depth=1 https://github.com/ix64/unlock-music.git . \
        && git submodule update --init --recursive \
        && npm install \
        && npm run build \
        && mv -f /root/unlock-music/dist /root/ \
        && cd /root \
        && wget https://github.com/Fan-chou/dockerfiles/raw/master/unlock-music/Caddyfile -O /root/Caddyfile \
        && rm -rf /root/unlock-music \
        && apk del git wget \
        && echo "Asia/Shanghai" > /etc/timezone
        
ENV TZ=Asia/Shanghai

CMD caddy -quic --conf /root/Caddyfile
