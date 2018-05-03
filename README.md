# kzisme-stacks 

Set set of Docker Stacks for kzisme

* Prometheus
* Grafana
* Node Exporter (*globally deployed*)

## Quick Start

1. Create the `prometheus` network.

```#!bash
$ docker network create -d overlay prometheus
```

2. Deploy the `mon` stack:

```#!bash
$ docker stack deploy -c mon.yml mon
```

You should end up with something like this:

```#!bash
$ docker stack ls
NAME                SERVICES
mon                 3

$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE                       PORTS
7vuf7u9tg9re        mon_grafana         replicated          1/1                 grafana/grafana:latest      *:3000->3000/tcp
dzedjnqzcsur        mon_node_exporter   global              1/1                 prom/node-exporter:latest
551qaassye06        mon_prometheus      replicated          1/1                 prom/prometheus:latest      *:9090->9090/tcp
```

And you should now have accessible Web interfaces to both Prometheus and
Grafana:

* http://192.168.99.100:9090/
* http://192.168.99.100:3000/

Tested with Docker Machine on OS X:

```#!bash
$ docker-machine create -d virtualbox default
```

Enjoy :)
