## start server

```
vagrant ssh server1
sudo nomad agent -config=/etc/nomad.d/server.hcl
```
## start clients
```
vagrant ssh client1
sudo nomad agent -config /etc/nomad.d/client.hcl
```
