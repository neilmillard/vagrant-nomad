## start server

```
vagrant ssh server1
sudo bash -c 'nomad agent -config=/etc/nomad.d/server.hcl >/var/log/nomad &'
```
## start clients
```
vagrant ssh client1
sudo nomad agent -config /etc/nomad.d/client.hcl
```

## start hashi-ui
```bash
nomad run /vagrant/hashi-ui/hashi-ui-docker.nomad
```
This will run a web interface on port 3000 on **one** of the client docker hosts.
[client1](http://192.168.50.3:3000) or [client2](http://192.168.50.4:3000)


## Ports Used
Nomad requires 3 different ports to work properly on servers and 2 on clients, some on TCP, UDP, or both protocols. Below we document the requirements for each port.

* ```HTTP API (Default 4646)```. This is used by clients and servers to serve the HTTP API. TCP only.
* ```RPC (Default 4647)```. This is used by servers and clients to communicate amongst each other. TCP only.
* ```Serf WAN (Default 4648)```. This is used by servers to gossip over the WAN to other servers. TCP and UDP.
