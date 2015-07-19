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


