## Overview

Elasticsearch and Kibana can be installed via downloading a tar archive, using homebrew or apt-get package managers or in Docker. 

### Tar archive

To run ES after donwloading run `bin/elasticsearch[kibana]` to start up the server. 

### Homebrew 

(Instrucctions)[https://logz.io/blog/brew-install-elasticsearch-mac/]

For Mac it will be installed in `/usr/local/Cellar/elasticsearch-full/7.13.2` and `/usr/local/Cellar/kibana-full/7.13.2`

Run `elasticsearch` or `kibana` from the terminal.

### Docker

(Instructions)[https://www.elastic.co/guide/en/kibana/current/docker.html]

```
docker network create elastic
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.13.2
docker run --name es01-test --net elastic -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.13.2
```

When ES is running you can run Kibana
```
docker pull docker.elastic.co/kibana/kibana:7.13.2
docker run --name kib01-test --net elastic -p 5601:5601 -e "ELASTICSEARCH_HOSTS=http://es01-test:9200" docker.elastic.co/kibana/kibana:7.13.2
```

#### Stop Docker containers

```
docker stop es01-test
docker stop kib01-test
```

To remove 

```
docker network rm elastic
docker rm es01-test
docker rm kib01-test
```

## Settings overview

### /bin

Contains binary scripts. 
`elasticsearch` starts up the server. 
`elasticsearch-plugin` and `elasticsearch-sql-cli` are used to install plugins and run SQL queries. 

### /config

This is where we configure ES

`elasticsearch.yml` is the main configuration file for the ES. All of the settings are commented out, meaning the default values are used.

* it's best practice to specify a cluster name `cluster.name: my-app`
* `node.name: node-1`
* `path.data` and `path.logs` enables to specify path to some directories. The default settings is to store them within the ES dir but it is a good practice to move them and configuration files out for the prod. It is usefull when updating ES.
* `network.host: 192.168.0.1` and `http.port: 9200` we can configure to bind a different host and port

`jvm.options`. You can configre memory size here (default 1 GB).

`log4j2.properties` used to configure logs

The rest of the files are used to configure users and roles. It is better to configure this in Kibana.

### /jdk

Contains the OpenJDK that ES ships with (Java Development Kit) it is a Java runtime used by ES (unless you have installed one yourseelf).

### /lib

Contains a number of dependencies that ES needs including log4j logging framework and Apache Lucine which EES builds on.

### /modules

Contains a number of built-in modules that provides some additional functionality.

### /plugins

Empty by default.

### $ES_HOME

Is an environment var that points to the root of the ES dir.


