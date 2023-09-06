---
description: tunnel all ports of running container on a remote server to localhost
---

# Tunnel all docker ports on remote server to localhost

#### tunnel.sh content

```bash
#!/bin/bash
SSH_SERVER=$1;

if [ -z $1 ] ; then
  echo "Usage: ./tunnel <ssh-server-name>" && exit 1;
fi

PORTS=$(ssh $SSH_SERVER docker ps --format "{{.Ports}}" |grep :| awk -F- '{print $1}'  | awk  -F: '{print $2}')
for PORT in $PORTS
do
	echo "tunneling port $PORT..."
	ssh -N -L $PORT:127.0.0.1:$PORT  $SSH_SERVER &
done
read -rsn1 -p"Press any key to exit";kill $(jobs -p);
ps S  | grep "ssh -N -L " | awk '{print $1}' |xargs kill -9
```



#### usage

```
chmod +x tunnel.sh
# Tunnel all port of containers run on remote server
./tunnel.sh ssh_remote_server

# Tunnel all port of containers & another port
./tunnel.sh ssh_remote_server 808 
```

