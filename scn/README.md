Official Blocknet Bitcoin Images
=================================

These scn docker images can be found on the docker hub: https://hub.docker.com/r/blocknetdx/scn/

scn
========

These scn images are optimized for use with the Blocknet DX.

**Note**

These images are _not a replacement or endorsement_ of the scn project (https://github.com/securecloudnet/SecureCloud).


Simple
======

Run a simple scn node on port 9190:
```
docker run -d --name=scn -p 9190:9190 blocknetdx/scn:latest
```


Persist blockchain w/ volumes
=============================

Run a scn node that persists the blockchain on a host directory. Recommended to avoid time consuming resyncs when updating to later container versions.
```
docker run -d --name=scn -p 9190:9190 -v=/crypto/scn/config:/opt/blockchain/config -v=/crypto/scn/data:/opt/blockchain/data blocknetdx/scn:0.17.0.1
```


Automatically restart the container
===================================

See https://docs.docker.com/engine/admin/start-containers-automatically/

`--restart=no|on-failure:retrycount|always|unless-stopped`

```
docker run -d --restart=no --name=scn -p 9190:9190 blocknetdx/scn:0.17.0.1 securecloudd -daemon=0 -rpcuser= -rpcpassword=123
docker run -d --restart=on-failure:10 --name=scn -p 9190:9190 blocknetdx/scn:0.17.0.1 securecloudd -daemon=0 -rpcuser= -rpcpassword=123
docker run -d --restart=unless-stopped --name=bitcoin -p 9190:9190 blocknetdx/scn:0.17.0.1 securecloudd -daemon=0 -rpcuser= -rpcpassword=123
docker run -d --restart=always --name=bitcoin -p 9190:9190 blocknetdx/scn:0.17.0.1 securecloudd -daemon=0 -rpcuser= -rpcpassword=123
```


Container shell access
======================

To login to the scn container and run RPC commands use the following command:
```
docker exec -it scn /bin/bash
```


Default securecloud.conf
=====================

The default configuration is below. A custom configuration file can be passed to the scn  node container through the `/opt/blockchain/config` volume. Some of these parameters can also be adjusted on the command line.
```
datadir=/opt/blockchain/data

dbcache=256
maxmempool=512

port=8333    # testnet: 18333
rpcport=8332 # testnet: 18332

listen=1
server=1
logtimestamps=1
logips=1

rpcallowip=127.0.0.1
rpctimeout=15
rpcclienttimeout=15
```


License
=======

This code is licensed under the Apache 2.0 License. Please refer to the [LICENSE](https://github.com/BlocknetDX/dockerimages/blob/master/LICENSE).