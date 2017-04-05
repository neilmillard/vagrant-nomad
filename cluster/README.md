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
