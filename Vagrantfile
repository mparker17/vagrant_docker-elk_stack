# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'socket'

# Set a default address for the logstash container.
logstash = Socket.ip_address_list.first.ip_address

Vagrant.configure(2) do |config|

  # Set up the Elasticsearch backend container.
  config.vm.define "elasticsearch" do |es|
    es.vm.provider "docker" do |d|
      d.image = "ehazlett/elasticsearch"
      d.name = "es"
      d.ports = [
        "9200:9200",
        "9300:9300"
      ]
    end
  end

  # Set up the Logstash middleware container.
  config.vm.define "logstash" do |ls|
    ls.vm.provider "docker" do |d|
      d.image = "ehazlett/logstash"
      #d.create_args = [
      #  "-f /etc/logstash.conf.sample"
      #]
      d.link("es:elasticsearch")
      d.ports = [
        "5000:5000",
        "5000:5000/udp"
      ]
    end

    # TODO: Find IP address of the logstash container.
    # logstash =
  end

  # Set up the Kibana front-end container.
  config.vm.define "kibana" do |k|
    k.vm.provider "docker" do |d|
      d.image = "ehazlett/kibana"
      d.ports = [
        "80:80"
      ]
    end
  end

  # Set up a logspout container so syslogs from Docker contaniers get forwarded
  # to logstash.
  config.vm.define "logspout" do |l|
    l.vm.provider "docker" do |d|
      d.image = "progrium/logspout"
      d.volumes = [
        "/var/run/docker.sock:/tmp/docker.sock"
      ]
      #d.create_args = [
      #  "syslog://" . sudo docker inspect -f '{{ .NetworkSettings.IPAddress }}' . ":5000"
      #]
    end
  end

end
