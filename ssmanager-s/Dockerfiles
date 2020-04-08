FROM alpine:3
MAINTAINER JackChou <dvfanzrfo@gmail.com>

WORKDIR /root

RUN set -ex \
        && runDeps="git build-base c-ares-dev autoconf automake libev-dev libtool libsodium-dev linux-headers mbedtls-dev pcre-dev" \
        && apk add --no-cache --virtual .build-deps ${runDeps} \
        && mkdir -p /root/libev \
        && cd /root/libev \
        && git clone --depth=1 https://github.com/shadowsocks/shadowsocks-libev.git . \
        && git submodule update --init --recursive \
        && ./autogen.sh \
	      && ./configure --prefix=/usr --disable-documentation \
	      && make install \
        && apk add --no-cache \
                  tzdata \
		              rng-tools \
		              ca-certificates \
                  npm \
		              $(scanelf --needed --nobanner /usr/bin/ss-* \
		              | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
		              | xargs -r apk info --installed \
		              | sort -u) \
        && apk del .build-deps \
        && cd /root \
        && rm -rf /root/libev \
        && npm i -g shadowsocks-manager --unsafe-perm \
        && echo "Asia/Shanghai" > /etc/timezone \

ENV TZ=Asia/Shanghai
CMD ["/usr/bin/ssmgr"]
