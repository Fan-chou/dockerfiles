FROM alpine:3
MAINTAINER JackChou <dvfanzrfo@gmail.com>

COPY default.conf /root/default.conf

WORKDIR /root

RUN set -ex \
        && apk add --no-cache npm git nodejs wget nginx \
        && mkdir -p /root/unlock-music \
        && cd /root/unlock-music \
        && git clone --depth=1 https://github.com/ix64/unlock-music.git . \
        && git submodule update --init --recursive \
        && npm install \
        && npm run build \
        && npm cache clean -f \
        && mv -f /root/unlock-music/dist /root/ \
        && cd /root \
        && mv -f /root/default.conf /etc/nginx/conf.d/default.conf \
        && mkdir /run/nginx \
        && rm -rf /root/unlock-music \
        && apk del git wget nodejs npm \
        && echo "Asia/Shanghai" > /etc/timezone
        
ENV TZ=Asia/Shanghai
 
CMD ["nginx", "-g", "daemon off;"]
