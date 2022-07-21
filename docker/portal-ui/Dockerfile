FROM nginx:1.23.0

ARG GRAVITEEIO_VERSION=3.4.2
ARG GRAVITEEIO_DOWNLOAD_URL=https://download.gravitee.io/graviteeio-apim/distributions

ENV WWW_TARGET /usr/share/nginx/html

RUN apt update -y \
  && apt install -y zip unzip netcat-openbsd wget \
  && wget ${GRAVITEEIO_DOWNLOAD_URL}/graviteeio-full-${GRAVITEEIO_VERSION}.zip -P /tmp \
  && unzip /tmp/graviteeio-full-${GRAVITEEIO_VERSION}.zip -d /tmp/ \
  && apt clean \
  && cp -fr /tmp/graviteeio-full-${GRAVITEEIO_VERSION}/graviteeio-portal-ui-${GRAVITEEIO_VERSION}/* ${WWW_TARGET} \
  && rm -rf /tmp/* \
  && ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log \
  && sed -i '/user  nginx;/d' /etc/nginx/nginx.conf \
  && sed -i 's,/var/run/nginx.pid,/tmp/nginx.pid,' /etc/nginx/nginx.conf \
  && sed -i "/^http {/a \    proxy_temp_path /tmp/proxy_temp;\n    client_body_temp_path /tmp/client_temp;\n    fastcgi_temp_path /tmp/fastcgi_temp;\n    uwsgi_temp_path /tmp/uwsgi_temp;\n    scgi_temp_path /tmp/scgi_temp;\n" /etc/nginx/nginx.conf \
  && chown -R 101:0 /usr/share/nginx /var/log/nginx /var/cache/nginx /etc/nginx /var/run \
  && chmod -R g+w /var/cache/nginx \
  && chmod -R g+w /etc/nginx

ADD config /etc/confd

COPY run.sh /run.sh

COPY bin/confd /bin

RUN chmod +x /bin/confd

CMD ["sh", "/run.sh"]
