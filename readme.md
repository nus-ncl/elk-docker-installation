# ELK for NCL - Docker Setup

![](https://img.shields.io/badge/docker-ready-brightgreen) 
![](https://img.shields.io/badge/docker--compose-ready-brightgreen) 
![](https://img.shields.io/badge/kubectl-ready-brightgreen) 
![](https://img.shields.io/badge/elastic-kibana-EC407A) 
![](https://img.shields.io/badge/elastic-elasticsearch-4CAF50)  
![](https://img.shields.io/badge/elastic-logstash-FFEB3B) 



## What's the ELK Stack?

<img src="https://www.elastic.co/static-res/images/elk/elk-stack-elkb-diagram.svg" style="width:70%;" />

**So, what is the ELK Stack?** "ELK" is the acronym for three open source projects: Elasticsearch,  Logstash, and Kibana. Elasticsearch is a search and analytics engine.  Logstash is a server‑side data processing pipeline that ingests data  from multiple sources simultaneously, transforms it, and then sends it  to a "stash" like Elasticsearch. Kibana lets users visualize data with  charts and graphs in Elasticsearch.

The Elastic Stack is the next evolution of the ELK Stack.


## What's ELK for NCL?

**ELK for NCL** is customized Elastic Stack to monitor different environment/platform in National Cybersecurity R&D Laboratory (NCL). The environments/platforms include:

- Orchestrator for Human Activity Generator - [OCTOBOT](https://github.com/nus-ncl/OctoBot) 
- Healthcare WebApp Environment based on this project - [NUSMed-WebApp](https://github.com/seanieyap/IFS4205-AY1920-S1-Team02-NUSMed-WebApp)
- and many more ...

## Preparation

Before we can start the dockerized ELK Stack, we need to configure the data ingestion which is mostly done by Logstash.

### Example for OCTOBOT

Because OCTOBOT use [Kubernetes](https://kubernetes.io) as the main orchestrator engine, so the collection will be done by Kubernetes metric collection, called `metricbeat-kubernetes`.
So, we need to run a specialized deployment [metricbeat-kubernetes.yaml](metricbeat/metricbeat-kubernetes.yaml) in the Kubernetes control plane using `kubectl` tools as shown below:

```bash
kubectl create -f metricbeat-kubernetes.yaml
```

### Example for Healthcare WebApp

In order to check the logs from the WebApp, Logstash need to make database query to MySQL database using JDBC for MySQL.
The detail configuration and pipeline for different Healthcare WebApp database, can be seen in [config](logstash/config) and [pipeline](logstash/pipeline) directory.
```yaml
input {
  jdbc {
    jdbc_driver_library => "/usr/share/java/mysql-connector-java.jar"
    jdbc_driver_class => "com.mysql.jdbc.Driver"
    jdbc_connection_string => "jdbc:mysql:/<MYSQL_SERVER>1:3306/<DATABASE_NAME>?serverTimezone=Asia/Singapore"
    jdbc_user => "<MYSQL_USER>"
    jdbc_password => "<MYSQL_PASSWORD>"
    parameters => {}
    schedule => "*/10 * * * *"
    statement => "select * from <TABLE_NAME>"
  }
}
```

## Quickstart Guide

Simply use docker-compose to start running the stack:

```bash
docker-compose up -d
```

if there is any problem running it just like this you might want to try it again with superuser permissions:

```bash
sudo docker-compose up -d
```



## FAQ

### How do I replace the JDBC connector?

To replace the JDBC container, simply replace the `.jar` file in `/logstash/jdbc` with a newer version, and rename it to `mysql-connector-java.jar`. Please do check if there is any incompatibility with the existing ELK stack versions, especially *Logstash*.



## Credits
[National Cybersecurity R&D Laboratory](https://ncl.sg)