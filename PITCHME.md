# KUBERNETES

---

## Agenda

* Infos
* Clusters
* Routes
 
---

# Infos

+++

version
```bash
matthiashaeussler@macbookmhs ~> kubectl version
Client Version: version.Info{Major:"1", Minor:"9", GitVersion:"v1.9.2", GitCommit:"5fa2db2bd46ac79e5e00a4e6ed24191080aa463b", GitTreeState:"clean", BuildDate:"2018-01-18T10:09:24Z", GoVersion:"go1.9.2", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"9", GitVersion:"v1.9.2", GitCommit:"5fa2db2bd46ac79e5e00a4e6ed24191080aa463b", GitTreeState:"clean", BuildDate:"2018-01-18T09:42:01Z", GoVersion:"go1.9.2", Compiler:"gc", Platform:"linux/amd64"}
``` 

---

# CLUSTERS

+++

List contexts

```bash
matthiashaeussler@macbookmhs ~> kubectl config get-contexts
CURRENT   NAME                 CLUSTER                      AUTHINFO             NAMESPACE
*         docker-for-desktop   docker-for-desktop-cluster   docker-for-desktop
          minikube             minikube                     minikube
```

+++

List clusters

```bash
matthiashaeussler@macbookmhs ~> kubectl config get-clusters
NAME
docker-for-desktop-cluster
minikube
```

+++

Full view

```bash
matthiashaeussler@macbookmhs ~> kubectl config view
apiVersion: v1
clusters:
- cluster:
    insecure-skip-tls-verify: true
    server: https://localhost:6443
  name: docker-for-desktop-cluster
- cluster:
    certificate-authority: /Users/matthiashaeussler/.minikube/ca.crt
    server: https://192.168.99.100:8443
  name: minikube
contexts:
- context:
    cluster: docker-for-desktop-cluster
    user: docker-for-desktop
  name: docker-for-desktop
- context:
    cluster: minikube
    user: minikube
  name: minikube
current-context: docker-for-desktop
kind: Config
preferences: {}
users:
- name: docker-for-desktop
  user:
    client-certificate-data: REDACTED
    client-key-data: REDACTED
- name: minikube
  user:
    client-certificate: /Users/matthiashaeussler/.minikube/client.crt
    client-key: /Users/matthiashaeussler/.minikube/client.key
```

+++

change context
```bash
matthiashaeussler@macbookmhs ~> kubectl config use-context docker-for-desktop
Switched to context "docker-for-desktop".
```

+++

switch context
```bash
matthiashaeussler@macbookmhs ~> kubectl get nodes
NAME                 STATUS    ROLES     AGE       VERSION
docker-for-desktop   Ready     master    2d        v1.9.2
matthiashaeussler@macbookmhs ~> kubectl config use-context minikube
Switched to context "minikube".
matthiashaeussler@macbookmhs ~> kubectl get nodes
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     <none>    61d       v1.8.0
```

---

# Minikube

+++

status
```bash
matthiashaeussler@macbookmhs ~> minikube status
There is a newer version of minikube available (v0.25.0).  Download it here:
https://github.com/kubernetes/minikube/releases/tag/v0.25.0

To disable this notification, run the following:
minikube config set WantUpdateNotification false
minikube: Stopped
cluster:
kubectl:
```

+++

version
```bash
matthiashaeussler@macbookmhs ~> minikube  version
minikube version: v0.24.1
```

+++

start
```bash
matthiashaeussler@macbookmhs ~> minikube start
Starting local Kubernetes v1.8.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
Loading cached images from config file.
```

+++

new status
```bash
matthiashaeussler@macbookmhs ~> minikube status
minikube: Running
cluster: Running
kubectl: Correctly Configured: pointing to minikube-vm at 192.168.99.100
```

+++

new context
```bash
matthiashaeussler@macbookmhs ~> kubectl config get-contexts                                                            Sun Feb 18 19:59:08 2018
CURRENT   NAME                 CLUSTER                      AUTHINFO             NAMESPACE
          docker-for-desktop   docker-for-desktop-cluster   docker-for-desktop
*         minikube             minikube                     minikube
```

+++
