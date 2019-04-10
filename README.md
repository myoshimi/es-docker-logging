# es-docker-logging

docker-compose.yml to accumulate logs by docker containers to Elasticsearch

=====

# Usage

* Build docker-compose.yml and launch containers
  * docker-compose.yml launches three containers, elasticsearch, fluentd and kibana
  * fluentd containers can accept forwarding logs by containers

```bash
git clone https://github.com/myoshimi/es-docker-logging
cd es-docker-logging
docker-compose build
docker-compose up -d
```

* Run some container with LogDriver options to forward logs to fluentd previously launched

```bash
docker run -d -p 80:80 \
    --log-driver=fluentd \
    --log-opt fluentd-address=localhost:24224 \
    --log-opt tag=docker.{{.Name}} nginx:latest
```

# Observation

* You can see and visualize containers logs via web browser in http://<path to docker host>:5601/.

