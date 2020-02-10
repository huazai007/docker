FROM alpine:latest
ENV ng_conf /usr/local/nginx
ADD nginx-1.14.2.tar.gz /usr/local/src/
ENV config="--prefix=/usr/local/nginx \
--user=nginx \
--group=nginx \
--with-http_ssl_module \
--with-http_gzip_static_module \
--with-http_image_filter_module \
--with-http_stub_status_module \
"
RUN addgroup -S nginx \
&&  adduser -D -S -h /var/cache/nginx/ -s /sbin/nologin -G nginx nginx \
&&  apk add --no-cache --virtual .build-deps \
gcc g++ pcre pcre-dev expat-dev perl zlib-dev libxml2-dev \
make  openssl openssl-dev bzip2-dev gd gd-dev \
&&  rm -rf /var/cache/apk/* \
&&  cd $ng_conf \
&&  ./configure $config \
&&  make && make install
expose 80 443
WORKDIR /usr/local/nginx/
ENTRYPOINT ["/sbin/nginx","-g","daemon off"]
