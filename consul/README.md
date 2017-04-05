# Consul
## start server

```
sudo bash -c 'consul agent -config-dir /etc/consul.d >/var/log/consul &'
```

The config includes the UI flag for the server.
[Consul UI](http://192.168.50.2:8500/ui)


# Ports used
Consul requires up to 5 different ports to work properly, some on TCP, UDP, or both protocols. Below we document the requirements for each port.

* ```Server RPC (Default 8300)```. This is used by servers to handle incoming requests from other agents. TCP only.
* ```Serf LAN (Default 8301)```. This is used to handle gossip in the LAN. Required by all agents. TCP and UDP.
* ```Serf WAN (Default 8302)```. This is used by servers to gossip over the WAN to other servers. TCP and UDP.
* ```CLI RPC (Default 8400)```. This is used by all agents to handle RPC from the CLI, but is deprecated in Consul 0.8 and later. TCP only. In Consul 0.8 all CLI commands were changed to use the HTTP API and the RPC interface was completely removed.
* ```HTTP API (Default 8500)```. This is used by clients to talk to the HTTP API. TCP only.
* ```DNS Interface (Default 8600)```. Used to resolve DNS queries. TCP and UDP.

Consul will also make an outgoing connection to HashiCorp's servers for Atlas-related features and to check for the availability of newer versions of Consul. This will be a TLS-secured TCP connection to scada.hashicorp.com:7223.
