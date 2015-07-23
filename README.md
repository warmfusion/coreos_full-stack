# Objective

* Fully load balanced cluster of N webservers delivering some basic dynamic PHP content
  * (Webpage showing name of server for example)
* Fault tolerant
  * 0 downtime on planned decomission of node 
  * <5 second window of 'failure' from services for unexpected failure

## Architecture

### 'Hardware'

* 2x CoreOS VMs
  * Running Fleet/ETCd for container management
* 1x F5-Big IP load balancer
  * Demo License

### Containers

* NGINX
* FPM-PHP
  * Serving content from a shared /src/ directory    
* Consul Cluster
  * To enable dynamic provisioning of configuration
* DockerHub
  * Using content from the /images/ directory

#### Optional Extensions

* Sensu
* Percona/MySQL datastore backend
* Memcached
* HAProxy (As alternative to F5)

## Implementation

3 Vagrant managed virtual machines running the 'Hardware' as defined in the Vagrantfile.


## Getting-Started

* SSH onto one of the core nodes and load up the various templates.

    fleetctl submit /mnt/templates/*
    # Start up the nginx and php containers
    fleetctl start {nginx,php-fpm}{,-discovery}@{1,2,3}
    
    # Lets get CONSUL started *everywhere*
    fleetctl start consul-agent

    fleetctl start consul-server@1

* Join consul-agents to the master by running a manual (at the moment) exec:

    SRV_IP=<IP Of the consul-server host>
    docker exec $( docker ps -f name=consul-agent -q) consul join $SRV_IP


### Auto-Discovery of Consul Servers

1. Start consul-server[-discovery]
    1. The discovery process writes the CORE_PRIVATE_IPv4 to etcd sharing the location of the consul-server
2. Start the consul-agent
    1. The systemd unit uses the etcdctl to get the consul-server location and auto-join at startup
3. Registrator then uses consul to record the existence of any new docker contains on any core-os host
    1. Uses the localhost port to talk to consul-agents
    2. Uses the docker socket to talk to docker


Issues: Running consul-server and consul-agent on the same ports clearly doesn't work 
   * I think  a server can be used as an agent, but i can't set a CONFLICTS rule for fleet against global services...
