# vagrant_docker-elk_stack

A Vagrantfile that sets up an Elasticsearch-Logstash-Kibana stack using Docker.

Note this is just a proof-of-concept. You very likely don't want to use this in a production environment.

This proof-of-concept aims to replicate the instructions in http://evanhazlett.com/2014/11/Logging-with-ELK-and-Docker/

# Usage

Before you start, you need to know whether you have to run Docker commands using `sudo` or not. If so, prefix all `vagrant` commands with `sudo` below.

1. From a terminal, run:

        vagrant up --no-parallel --provider docker
