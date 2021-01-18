FROM adoptopenjdk/openjdk11:armv7l-debian-jre11u-nightly

RUN apt update -y
RUN apt install -y curl nginx

# SETUP NGINX PROXY

COPY default.nginx.conf /etc/nginx/sites-available/default

# SETUP ELASTIC 7.5.1
WORKDIR /opt

RUN curl -o elastic.tar.gz https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.5.1-no-jdk-linux-x86_64.tar.gz && \
	tar zxvf elastic.tar.gz && \
	rm elastic.tar.gz
	
WORKDIR /opt/elasticsearch-7.5.1

# UPDATE CONFIG
RUN echo "http.port: 9292" >> config/elasticsearch.yml
RUN echo "network.host: 127.0.0.1" >> config/elasticsearch.yml
RUN echo "xpack.ml.enabled: false" >> config/elasticsearch.yml

COPY docker-entrypoint.sh /opt/

RUN chmod +x /opt/docker-entrypoint.sh

ENTRYPOINT ["/opt/docker-entrypoint.sh"]
