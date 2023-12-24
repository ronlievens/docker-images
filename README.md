# Authentication

## Keycloak

Start: `docker-compose -f authentication/keycloak/docker-compose.yaml up -d`
Stop: `docker-compose -f authentication/keycloak/docker-compose.yaml down`
Dashboard: http://127.0.0.1:18080/

# Building

## Jenkins with Sonar

Start: `docker-compose -f building/jenkins_sonar/docker-compose.yaml up -d`
Stop: `docker-compose -f building/jenkins_sonar/docker-compose.yaml down`
Dashboard:

- http://127.0.0.1:7080/jenkins/
- http://127.0.0.1:9000/sonarqube/

### Install plugins [SonarQube Community multi-branch plugin](https://github.com/mc1arke/sonarqube-community-branch-plugin)

Download [sonarqube-community-branch-plugin](https://github.com/mc1arke/sonarqube-community-branch-plugin/releases/download/1.3.2/sonarqube-community-branch-plugin-1.3.2.jar)
into the folder `data\sonarqube\plugins`.
Check if the versions match the versions in the `docker-compose.yaml` file.

# Databases

## IBM DB2

Start: `docker-compose -f databases/db2/docker-compose.yaml up -d`
Stop: `docker-compose -f databases/db2/docker-compose.yaml down`

## Mariadb

Start: `docker-compose -f databases/mariadb/docker-compose.yaml up -d`
Stop: `docker-compose -f databases/mariadb/docker-compose.yaml down`

## Oracle XE

Start: `docker-compose -f databases/oracle-xe/docker-compose.yaml up -d`
Stop: `docker-compose -f databases/oracle-xe/docker-compose.yaml down`

To connect to Oracle XE use the url: `jdbc:oracle:thin:@localhost:1521/PDB1`
In Intellij, choose `Connection type`:`URL only` and enter the url above.

## Postgresql

Start: `docker-compose -f databases/postgresql/docker-compose.yaml up -d`
Stop: `docker-compose -f databases/postgresql/docker-compose.yaml down`

# Mail

## Mailhog

Start: `docker-compose -f mailing/mailhog/docker-compose.yaml up -d`
Stop: `docker-compose -f mailing/mailhog/docker-compose.yaml down`
Dashboard: http://127.0.0.1:9025/mailhog/

# Messaging

## IBM MQ

Start: `docker-compose -f messaging/ibm-mq/docker-compose.yaml up -d`
Stop: `docker-compose -f messaging/ibm-mq/docker-compose.yaml down`
Dashboard (admin/passw0rd): https://127.0.0.1:9443/ibmmq/console/

# Monitoring

## ELK

Start: `docker-compose -f monitoring/elk/docker-compose.yaml up -d`
Stop: `docker-compose -f monitoring/elk/docker-compose.yaml down`
Dashboard: http://127.0.0.1:5601/kibana/

## Grafana

Start: `docker-compose -f monitoring/grafana/docker-compose.yaml up -d`
Stop: `docker-compose -f monitoring/grafana/docker-compose.yaml down`
Dashboard: http://127.0.0.1:3000/grafana/

## Jaeger

Start: `docker-compose -f monitoring/jaeger/docker-compose.yaml up -d`
Stop: `docker-compose -f monitoring/jaeger/docker-compose.yaml down`
Dashboard: http://127.0.0.1:16686/jaeger/

## Prometheus

Documentation:

- [Spring Boot Actuator metrics monitoring with Prometheus and Grafana](https://www.callicoder.com/spring-boot-actuator-metrics-monitoring-dashboard-prometheus-grafana/)
- [Prometheus CLI options](https://gist.github.com/0x0I/eec137d55a26a16d836b84cbc186ab52#file-prometheus-cli-options-L18)
- [Prometheus MANAGEMENT API](https://prometheus.io/docs/prometheus/latest/management_api/)
- [Docker hub - Prometheus](https://hub.docker.com/r/prom/prometheus/)

Start: `docker-compose -f monitoring/prometheus/docker-compose.yaml up -d`
Stop: `docker-compose -f monitoring/prometheus/docker-compose.yaml down`
Dashboard: http://127.0.0.1:9090/prometheus/
Health dashboard: (http://localhost:9090/-/healthy)

### example prometheus.yml

The `host.docker.internal` is to connect to the `localhost` from a docker image.

```yaml
scrape_configs:
    -   job_name: 'Spring boot example on localhost'
        metrics_path: '/api/actuator/prometheus'
        scrape_interval: 5s
        static_configs:
            -   targets: [ 'host.docker.internal:8080' ]
    -   job_name: 'Golang with Echo example on localhost'
        metrics_path: '/metrics'
        scrape_interval: 5s
        static_configs:
            -   targets: [ 'host.docker.internal:1323' ]

```
