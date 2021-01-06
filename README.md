# Getting Started with KinD 

<a href=https://player.vimeo.com/video/497069850>
<img src=https://user-images.githubusercontent.com/755710/103590174-2619ad80-4ebb-11eb-939f-9fe59924c9fd.png width=400 />
</a>





# Step 1

Install kind

```bash

GO111MODULE="on" go get sigs.k8s.io/kind

```


# Step 2

Create cluster

```bash

kind create cluster --config configs/kind_basic.yaml
```

# Step 3

Install metal

```bash

# Metal
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.5/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.5/manifests/metallb.yaml
# On first install only
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"


kubectl apply -f configs/metal.yaml 


```


# Nginx


```bash

cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - name: nginx 
    image: nginx
    ports:
    - containerPort: 80
EOF


```

# LoadBalancer

```bash

kubectl expose pod nginx --type=LoadBalancer

```


   
# After it is installed


```bash


kubectl exec -it nginx -- bash
apt-get update
apt-get install -y procps
apt-get install -y net-tools

```

Also, since KinD uses kubeadm, you may want to inspect the config. 


```bash
docker exec -it kind-control-plane cat /kind/kubeadm.conf

```


If needed, you can dump logs to a folder.  Here' I'm dumping
to the folder *dumpFolder*.

```bash
kind export logs dumpFolder

```





## Forward a port


shft-cmd-p

