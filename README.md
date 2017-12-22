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



## Chapter 6:Introduction to the Cassandra Query Language
### Working with Keyspace

The real purpose of a keyspace is to act as a namespace that specifies how cassandra replicates data.  
This means that if you have different sets of data that differ in their replication requirements, you can use different keyspaces to store the data.  
__You control cassandra's data replication on a per-keyspace basis__  
__use a single keyspace for each application__  


### Creating a Keyspace
For production purposes, you must use
```
NetworkTopologyStrategy
```
like
```
{'class':'NetworkTopologyStrategy','DC1':1,'DC2':3} AND durble_writes = true;
```

### Altering a Keyspace
```
alter keyspace "cycle" with replication ={'class':'','replication_factor':''};
```
you cant alter the name of keyspace.

###### alter NetworkTopologyStrategy
```
alter keyspace cycle with replication = {};
nodetool repair -full
```
```
The write throughput of the cluster is inversely related to the replication factor
```

### Preventing a Keyspace from Sending Replicas to Some Data Centers
```
alter keyspace cycle with replication ={'class':'NetworkTopologyStrategy','dc1':3,'dc2':0,'dc3':3};
```

### Removing a Keyspace
```
DROP KEYSPACE cycle;
describe keyspaces;
```
