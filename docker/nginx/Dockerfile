FROM nginx:1.15

RUN usermod -u 1000 www-data

ADD /docker/nginx/nginx.conf /etc/nginx/nginx.conf
ADD /docker/nginx/server.conf /etc/nginx/conf.d/

EXPOSE 80
EXPOSE 443