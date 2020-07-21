# ELK for NCL - Docker Setup

![](https://img.shields.io/badge/docker-ready-brightgreen)![](https://img.shields.io/badge/docker--compose-ready-brightgreen)![](https://img.shields.io/badge/kubectl-ready-brightgreen)

![](https://img.shields.io/badge/elastic-kibana-EC407A)![](https://img.shields.io/badge/elastic-elasticsearch-4CAF50)![](https://img.shields.io/badge/elastic-logstash-FFEB3B)



## What's the ELK Stack?

<img src="https://www.elastic.co/static-res/images/elk/elk-stack-elkb-diagram.svg" style="width:70%;" />

**So, what is the ELK Stack?** "ELK" is the acronym for three open source projects: Elasticsearch,  Logstash, and Kibana. Elasticsearch is a search and analytics engine.  Logstash is a server‑side data processing pipeline that ingests data  from multiple sources simultaneously, transforms it, and then sends it  to a "stash" like Elasticsearch. Kibana lets users visualize data with  charts and graphs in Elasticsearch.

The Elastic Stack is the next evolution of the ELK Stack.



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
[National Cybersecurity R&D Laboratories](https://ncl.sg/pricing)