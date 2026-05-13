FROM alpine:3.21

ENV WEBPROC_VERSION=0.4.0

RUN apk update && apk --no-cache add dnsmasq \
    && apk add --no-cache --virtual .build-deps curl \
    && ARCH="$(uname -m)" \
    && case "$ARCH" in \
         x86_64)  WEBPROC_ARCH="amd64" ;; \
         aarch64) WEBPROC_ARCH="arm64" ;; \
         armv7l)  WEBPROC_ARCH="armv7" ;; \
         armv6l)  WEBPROC_ARCH="armv6" ;; \
         *)       echo "Unsupported arch: $ARCH" && exit 1 ;; \
       esac \
    && curl -sL "https://github.com/jpillora/webproc/releases/download/v${WEBPROC_VERSION}/webproc_${WEBPROC_VERSION}_linux_${WEBPROC_ARCH}.gz" \
       | gzip -d > /usr/local/bin/webproc \
    && chmod +x /usr/local/bin/webproc \
    && apk del .build-deps

RUN mkdir -p /etc/default/ \
    && echo -e "ENABLED=1\nIGNORE_RESOLVCONF=yes" > /etc/default/dnsmasq

COPY dnsmasq.conf /etc/dnsmasq.conf

ENTRYPOINT ["webproc", "--config", "/etc/dnsmasq.conf", "--", "dnsmasq", "--no-daemon"]
