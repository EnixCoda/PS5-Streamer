FROM alpine

# Uncomment below RUN if you are inside mainland China, it is used to resolve github.com
# RUN echo "nameserver 114.114.114.114" > /etc/resolv.conf

WORKDIR /opt

# Combine commands in single RUN to reduce image size (60MB vs 200MB+)
RUN \
    # Install deps
    apk add --update build-base libressl-dev && \
    # Get nginx and rtmp
    wget -O nginx.tar.gz https://nginx.org/download/nginx-1.20.2.tar.gz && \
    tar zxvf nginx.tar.gz && \
    wget -O nginx-rtmp-module.zip https://github.com/arut/nginx-rtmp-module/archive/refs/heads/master.zip && \
    unzip nginx-rtmp-module.zip && \
    cd /opt/nginx-1.20.2 && \
    # Build & install nginx
    ./configure --prefix=/opt/nginx --add-module=../nginx-rtmp-module-master --with-http_ssl_module --without-http_rewrite_module --without-http_gzip_module && \
    make && \
    make install && \
    cp /opt/nginx-rtmp-module-master/stat.xsl /opt/nginx/html/ && \
    # Clean up
    cd /opt && \
    rm -rf nginx.tar.gz nginx-1.20.2 nginx-rtmp-module.zip nginx-rtmp-module-master && \
    apk del build-base

# Configure nginx
ADD nginx.conf /opt/nginx/conf/nginx.conf

CMD [  "/opt/nginx/sbin/nginx", "-g", "daemon off;" ]
