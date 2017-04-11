# vagrant-nomad
Testing nomad with their getting started guide

The cluster folder contains sample config for a 1 master, 2 worker cluster.

This needs fileshare enabled. This requires VB Guest Additions.  
The easiest way to install this is via the vbguest plugin.
```
vagrant gem install vagrant-vbguest
```

Then run 
```bash
vagrant up
```