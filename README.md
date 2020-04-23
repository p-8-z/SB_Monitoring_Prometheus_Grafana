# Spring Apps Monitoring

Here's a quick start using Docker-Compose to start-up a Prometheus stack 
containing Prometheus, Grafana to monitor your Spring infrastructure. 

## Spring Apps

Should expose actuator on url `/actuator/prometheus`

## Prometheus

The Prometheus monitoring system and time series database.

[Page](https://prometheus.io/)

[Configuration](https://prometheus.io/docs/prometheus/latest/configuration/configuration/)

[Github](https://github.com/prometheus/prometheus)

All configuration is in `prometheus.yml` file.

## Grafana

The tool for beautiful monitoring and metric analytics & dashboards for Graphite, 
InfluxDB & Prometheus & More 

[Page](https://grafana.com)

[Configuration](https://grafana.com/docs/grafana/latest/installation/configuration/)

[Github](https://github.com/grafana/grafana)


## Consul

Distributed, highly available, and data center aware solution 
to connect and configure applications across dynamic, distributed infrastructure.

[Page](https://www.consul.io)

[Configuration](https://www.consul.io/docs/agent/options.html)

[Github](https://github.com/hashicorp/consul)

## How to

Add libraries to your Spring Applications.
```xml
<dependencies>
    ...
    <!--   Actuator Starter     -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <!--   Micrometer Dependecies     -->
    <dependency>
        <groupId>io.micrometer</groupId>
        <artifactId>micrometer-core</artifactId>
        <version>${micrometer.version}</version>
    </dependency>
    <dependency>
        <groupId>io.micrometer</groupId>
        <artifactId>micrometer-registry-prometheus</artifactId>
        <version>${micrometer.version}</version>
    </dependency>
    ...
</dependencies>
```

Configure `prometheus.yml` so its Gathering services from Consul Service Discovery and
requesting data from Services Actuator.
```yaml
scrape_configs:
  - job_name: 'prometheus'
    metrics_path: /actuator/prometheus
    consul_sd_configs:
      - server: 'consul:8500'
    relabel_configs:
      - source_labels: [__meta_consul_service]
        target_label:  application
```
Start Docker-Compose
```cmd
docker-compose up
```

## Resources 

    A docker-compose stack for Prometheus monitoring 
    
    Prometheus, Grafana and Node scraper to monitor your Docker infrastructure
    
    -> [Git Repo](https://github.com/vegasbrianc/prometheus)

## About

Creator p8z

