FROM adoptopenjdk/openjdk11:armv7l-centos-jre-11.0.8_10

ARG GRAVITEEIO_VERSION=3.4.2
ARG GRAVITEEIO_DOWNLOAD_URL=https://download.gravitee.io/graviteeio-apim/distributions
ENV GRAVITEEIO_HOME /opt/graviteeio-gateway

RUN yum update -y 
RUN yum install -y zip unzip netcat-openbsd wget
RUN wget ${GRAVITEEIO_DOWNLOAD_URL}/graviteeio-full-${GRAVITEEIO_VERSION}.zip --no-check-certificate -P /tmp
RUN unzip /tmp/graviteeio-full-${GRAVITEEIO_VERSION}.zip -d /tmp/ 
RUN yum clean all
RUN mv /tmp/graviteeio-full-${GRAVITEEIO_VERSION}/graviteeio-gateway* ${GRAVITEEIO_HOME} 
RUN rm -rf /tmp/* 
RUN chgrp -R 0 ${GRAVITEEIO_HOME} 
RUN chmod -R g=u ${GRAVITEEIO_HOME}

WORKDIR ${GRAVITEEIO_HOME}
EXPOSE 8082
ENTRYPOINT ["./bin/gravitee"]
