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

+++

```bash
matthiashaeussler@macbookmhs ~/g/C/ToDoCommandService> kubectl get componentstatuses
NAME                 STATUS    MESSAGE              ERROR
controller-manager   Healthy   ok
scheduler            Healthy   ok
etcd-0               Healthy   {"health": "true"}
``` 

+++

```bash
matthiashaeussler@macbookmhs ~/g/C/ToDoCommandService> kubectl get nodes
NAME                 STATUS    ROLES     AGE       VERSION
docker-for-desktop   Ready     master    9d        v1.9.2
``` 

+++

```bash
matthiashaeussler@macbookmhs ~/g/C/ToDoCommandService> kubectl describe nodes docker-for-desktop
Name:               docker-for-desktop
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/hostname=docker-for-desktop
                    node-role.kubernetes.io/master=
Annotations:        node.alpha.kubernetes.io/ttl=0
                    volumes.kubernetes.io/controller-managed-attach-detach=true
Taints:             <none>
CreationTimestamp:  Fri, 16 Feb 2018 11:22:40 +0100



Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  OutOfDisk        False   Sun, 25 Feb 2018 21:23:35 +0100   Fri, 16 Feb 2018 11:22:36 +0100   KubeletHasSufficientDisk     kubelet has sufficient disk space available
  MemoryPressure   False   Sun, 25 Feb 2018 21:23:35 +0100   Tue, 20 Feb 2018 19:18:42 +0100   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Sun, 25 Feb 2018 21:23:35 +0100   Tue, 20 Feb 2018 19:18:42 +0100   KubeletHasNoDiskPressure     kubelet has no disk pressure
  Ready            True    Sun, 25 Feb 2018 21:23:35 +0100   Tue, 20 Feb 2018 19:18:42 +0100   KubeletReady                 kubelet is posting ready status



Addresses:
  InternalIP:  192.168.65.3
  Hostname:    docker-for-desktop
Capacity:
 cpu:     4
 memory:  6100260Ki
 pods:    110
Allocatable:
 cpu:     4
 memory:  5997860Ki
 pods:    110
System Info:
 Machine ID:
 System UUID:                F36441E9-0000-0000-AC52-A0BD6FC8BE2F
 Boot ID:                    72ccfec3-5ff8-4485-be74-a0d8b22cbad3
 Kernel Version:             4.9.75-linuxkit-aufs
 OS Image:                   Docker for Mac
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://18.2.0
 Kubelet Version:            v1.9.2
 Kube-Proxy Version:         v1.9.2
ExternalID:                  docker-for-desktop



Non-terminated Pods:         (15 in total)
  Namespace                  Name                                          CPU Requests  CPU Limits  Memory Requests  Memory Limits
  ---------                  ----                                          ------------  ----------  ---------------  -------------
  docker                     compose-54975bf945-79w8d                      0 (0%)        0 (0%)      0 (0%)           0 (0%)
  docker                     compose-api-6b9ddf57b6-xt79n                  0 (0%)        0 (0%)      0 (0%)           0 (0%)
  kube-system                etcd-docker-for-desktop                       0 (0%)        0 (0%)      0 (0%)           0 (0%)
  kube-system                kube-apiserver-docker-for-desktop             250m (6%)     0 (0%)      0 (0%)           0 (0%)
  kube-system                kube-controller-manager-docker-for-desktop    200m (5%)     0 (0%)      0 (0%)           0 (0%)
  kube-system                kube-dns-6f4fd4bdf-65kkk                      260m (6%)     0 (0%)      110Mi (1%)       170Mi (2%)
  kube-system                kube-proxy-b2tcg                              0 (0%)        0 (0%)      0 (0%)           0 (0%)
  kube-system                kube-scheduler-docker-for-desktop             100m (2%)     0 (0%)      0 (0%)           0 (0%)
  kube-system                kubernetes-dashboard-5bd6f767c7-zc76v         0 (0%)        0 (0%)      0 (0%)           0 (0%)
  todo-cn-app                todo-db-79fff98d5-v26pq                       0 (0%)        0 (0%)      0 (0%)           0 (0%)
  todo-cn-app                todo-messaging-6477f9bd79-2cmsb               0 (0%)        0 (0%)      0 (0%)           0 (0%)
  todo-cn-app                todocommandservice-54cbc76d6-vljgv            0 (0%)        0 (0%)      0 (0%)           0 (0%)
  todo-cn-app                todoqueryservice-545dc94dcb-wbqrp             0 (0%)        0 (0%)      0 (0%)           0 (0%)
  todo-cn-app                todoserviceregistry-5b8766c57f-h9nm8          0 (0%)        0 (0%)      0 (0%)           0 (0%)
  todo-cn-app                todouiservice-67c888ccb-qv785                 0 (0%)        0 (0%)      0 (0%)           0 (0%)



Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  CPU Requests  CPU Limits  Memory Requests  Memory Limits
  ------------  ----------  ---------------  -------------
  810m (20%)    0 (0%)      110Mi (1%)       170Mi (2%)



Events:
  Type    Reason                   Age                From                         Message
  ----    ------                   ----               ----                         -------
  Normal  Starting                 11h                kubelet, docker-for-desktop  Starting kubelet.
  Normal  NodeAllocatableEnforced  11h                kubelet, docker-for-desktop  Updated Node Allocatable limit across pods
  Normal  NodeHasSufficientDisk    11h (x8 over 11h)  kubelet, docker-for-desktop  Node docker-for-desktop status is now: NodeHasSufficientDisk
  Normal  NodeHasSufficientMemory  11h (x8 over 11h)  kubelet, docker-for-desktop  Node docker-for-desktop status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    11h (x7 over 11h)  kubelet, docker-for-desktop  Node docker-for-desktop status is now: NodeHasNoDiskPressure
``` 

+++

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

stop
```bash
matthiashaeussler@macbookmhs ~> minikube stop
Stopping local Kubernetes cluster...
Machine stopped.
```

---

### Dashboard

+++

install
```bash
matthiashaeussler@macbookmhs ~/g/m/kubernetes>kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml

secret "kubernetes-dashboard-certs" created
serviceaccount "kubernetes-dashboard" created
role "kubernetes-dashboard-minimal" created
rolebinding "kubernetes-dashboard-minimal" created
deployment "kubernetes-dashboard" created
service "kubernetes-dashboard" created
``` 
+++

create proxy
```bash
matthiashaeussler@macbookmhs ~/g/m/kubernetes> kubectl proxy --port=8765
Starting to serve on 127.0.0.1:8765

matthiashaeussler@macbookmhs ~/g/m/kubernetes> curl localhost:8765
```

+++

API enpdpoints
```json
{
  "paths": [
    "/api",
    "/api/v1",
    "/apis",
    "/apis/",
    "/apis/admissionregistration.k8s.io",
    "/apis/admissionregistration.k8s.io/v1beta1"
}
```

+++
