FROM nginx:latest

USER root

WORKDIR /server/

COPY server/server.c /server/

COPY nginx/nginx.conf /etc/nginx/nginx.conf

RUN apt update && \
    apt-get install -y libfcgi-dev && \
    apt-get install -y spawn-fcgi && \
    apt-get install -y gcc

ENTRYPOINT gcc server.c -lfcgi -o server && \
    spawn-fcgi -p 8080 ./server && \
       nginx -g 'daemon off;' 