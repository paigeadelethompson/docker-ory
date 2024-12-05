# Unmaintained / shelved 
until further notice

# Docker Ory
This environment sets up a full Ory environment (Hydra, Kratos, Keto, OathKeeper, and the self service UI) for setting up and running your own OpenID infrastructure. 
It includes setting up a production valid CockroachDB cluster. It is reccomended that you use a clean VM and a dedicated install of Docker
with the provided Docker and NFTables configuration detailed in this README.


## Docker daemon configuration 
This project doesn't rely on docker for iptables configuration. Instead, an nftables configuration has been provided in 
`config/etc/nftables/nftables.conf` 

- install nftables and use the provided configuration
- configure docker, either: `/etc/default/docker` or `/etc/sysconfig/docker`
```
DOCKER_OPTS="--ipv6=false --iptables=false --ip-masq=false --bip=100.64.60.1/22 --fixed-cidr=100.64.60.0/22 --default-address-pool base=100.64.64.0/20,size=29"
```
- Copy `config/docker/examples/env` to `config/docker/.env` and edit it
- For various reasons keto and kratos require configuration files that can't be specified in the env so edit `config/keto/keto.yml` and `config/kratos/config.yml`
- Run `./up` to start a new cockroach cluster and all of the Ory daemons

To stop the cluster: 
- Run `./down`

To delete ephemeral volumes: 
- `docker volume prune -f`
