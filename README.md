# vagrant-nomad
Testing nomad with their getting started guide

The cluster folder contains sample config for a 1 master, 2 worker cluster.

# Ports Used
Nomad requires 3 different ports to work properly on servers and 2 on clients, some on TCP, UDP, or both protocols. Below we document the requirements for each port.

* HTTP API (Default 4646). This is used by clients and servers to serve the HTTP API. TCP only.

* RPC (Default 4647). This is used by servers and clients to communicate amongst each other. TCP only.

* Serf WAN (Default 4648). This is used by servers to gossip over the WAN to other servers. TCP and UDP.