# abexportapcassandraadmin

#### Disable the zone_reclaim_mode on NUMA Systems
```
cat /proc/sys/vm/zone_reclaim_mode  #must 0
```
edit
```
vim /etc/sysctl.conf
```
edit
```
net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
net.core.rmem_default = 16777216
```
```
sysctl -p /etc/sysctl.conf
```

```
vim /etc/security/limits.conf
```
edit
```
user - memlock unlimited
user - nofile 100000
user - nproc 32768
user - as unimited
```


#### Selecting the Nodes to Serve as Seed Nodes
cassandra.yaml
```
seed_provider:
  - class_name: 
  - seeds: "192.168.1.1,192.168.1.3"
```
