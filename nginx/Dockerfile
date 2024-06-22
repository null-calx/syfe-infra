FROM debian:bookworm

RUN apt-get update && apt-get install -y \
    wget build-essential libpq-dev libpcre3-dev libssl-dev zlib1g-dev

RUN wget -q https://openresty.org/download/openresty-1.25.3.1.tar.gz && \
    tar xf openresty-1.25.3.1.tar.gz && \
    cd openresty-1.25.3.1/ && \
    ./configure --prefix=/opt/openresty \
                --with-pcre-jit \
                --with-ipv6 \
                --without-http_redis2_module \
                --with-http_iconv_module \
                --with-http_postgres_module -j8 && \
    make && make install

RUN mkdir -p /etc/nginx

COPY ./nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["/opt/openresty/nginx/sbin/nginx", \
    "-c", "/etc/nginx/nginx.conf", \
    "-g", "daemon off;"]
