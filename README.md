# Kubernetes Flex Volume Archive
Driver for mounting tar.gz archives as a Kubernetes Volume.


## Install
Copy script to `/usr/libexec/kubernetes/kubelet-plugins/volume/exec/almonteb~archive/archive`

> NOTE: On driver initialization, the node will install [jq](https://github.com/stedolan/jq) if not already present in your `$PATH`.

## Usage
### Sample Pod
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: default
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: data
      mountPath: /usr/share/nginx/html
    ports:
    - containerPort: 80
  volumes:
  - name: data
    flexVolume:
      driver: "almonteb/archive"
      options:
        archive: "https://gist.github.com/almonteb/94c37f8a5ad1b1b615a2472520296a5b/archive/2ef0acfe26776d10b9bc80ca8bc07558be01f841.tar.gz"
```