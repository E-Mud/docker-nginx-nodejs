FROM node:7

RUN apt-get update
RUN apt-get -y install nginx gettext-base

COPY tmpl.default.conf /etc/nginx/
COPY setup-nginx /usr/local/bin/

ENV REPLACE_DEFAULT=true \
  NGINX_SITE_FILE="/etc/nginx/tmpl.default.conf" \
  NGINX_PORT=80 \
  NGINX_SERVER_NAME=_ \
  NGINX_ROOT="/var/www/html" \
  NGINX_INDEX="index index.html index.htm index.nginx-debian.html"

ENTRYPOINT ["setup-nginx"]
CMD ["nginx", "-g", "daemon off;"]
