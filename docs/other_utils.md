
# Common utils

```bash

sudo apt-get install -y bridge-utils
sudo apt-get install -y haproxy

```

# Edit config settings

```bash

sudo vi /etc/haproxy/haproxy.cfg


```



```yaml
frontend http_front
   bind *:80
   stats uri /haproxy?stats
   default_backend http_back

backend http_back
   balance roundrobin
   server <server1 name> <private IP 1>:80 check
   server <server2 name> <private IP 2>:80 check
```

So... we could use

```yaml
# Our server settings

frontend http_front
   bind *:3000
   stats uri /haproxy?stats
   default_backend http_back

backend http_back
   balance roundrobin
   server nginx 172.18.1.128:80 check
   
```

# Start

```bash
sudo service haproxy start

```

## Forward a port in codespaces


shft-cmd-p



## Ubuntu

```bash

# Create ubuntu
kubectl run --rm -i --tty ubuntu --image=ubuntu:latest --restart=Never -- bash -il

# Attach to it later
kubectl exec -it ubuntu -- /bin/bash

```