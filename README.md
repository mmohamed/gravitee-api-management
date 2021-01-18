# Gravitee API Management for k8S and armhf

<p align="center">
<img src="https://demo.gravitee.io/themes/assets/GRAVITEE_LOGO1-01.png" width="250">
</p>

----

Gravitee Component:

1. Docker Images : 
- [Gateway 3.4.2](docker/gateway/Dockerfile) - https://hub.docker.com/repository/docker/medinvention/gravitee-gateway
- [Management-API 3.4.2](docker/management-api/Dockerfile) - https://hub.docker.com/repository/docker/medinvention/gravitee-management-api
- [Management-UI 3.4.2](docker/management-ui/Dockerfile) - https://hub.docker.com/repository/docker/medinvention/gravitee-management-api
- [Portal-UI 3.4.2](docker/portal-ui/Dockerfile) - https://hub.docker.com/repository/docker/medinvention/portal-ui


2. Dependencies :
- [ElasticSearch 7.5.1](docker/elastic/Dockerfile) - https://hub.docker.com/repository/docker/medinvention/elastic
- MongoDB 3.2.10 - https://hub.docker.com/repository/docker/medinvention/mongodb

3. Deployments:
- Create **graviteeio** namespace
- TLS Secret: create your own TLS Secret file from [api-tls.yaml.dist](k8s/api-tls.yaml.dist)
- ElasticSearch : with Single Node, apply [elastic.yaml](k8s/elastic.yaml)
- MonogDB instance : apply [mongodb.yaml](k8s/mongodb.yaml)
- Pull Chart : 
    ```
    helm repo add graviteeio https://helm.gravitee.io
    helm pull graviteeio/apim3 --version "3.0.15"
    ```
- Extract : ``tar -xvf apim3-3.0.15.tgz``
- Create your own values files from [template](graviteeio-values.yaml.dist) 
- Install ``helm install -f graviteeio-values.yaml -n graviteeio graviteeio apim3\``


**NOTA** : For Management and Portal image building, a Confd binary is used, it's loaded from Docker context, [builded for armhf with v0.16.0](https://github.com/kelseyhightower/confd/tree/v0.16.0) 

---- 

[*More informations*](https://blog.medinvention.dev)

