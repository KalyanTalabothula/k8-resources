k8 architecture
--------------------
master and nodes

master
===========
api server --> all  cluster interactions comes to api server. validates RBAC and provide the response. if you are creating pods, api server validates and handover to scheduler.

scheduler --> it a component to decide where your pod should run. it checks for taints and tolerations, selectors like nodeaffinity, pod affinity, node readiness,etc.

control manager
replica controller -> make sures desired number of pod replicas run all the time.
node controller --> checks desired number of nodes are running
Job controller --> A Job runs a Pod (or multiple Pods) until the work is finished successfully — then it stops.
ServiceAccount controller --> Create default ServiceAccounts for new namespaces.
EndpointSlice controller -> Populates EndpointSlice objects (to provide a link between Services and Pods).

etcd --> key value storage for k8 cluster. all k8 configs are here
🧠 What is etcd in Kubernetes?

➡️ etcd is a key–value database that stores all the cluster data of Kubernetes.

💬 In simple words:

etcd is like Kubernetes’s brain 🧠 —
it remembers everything about your cluster (nodes, pods, configs, secrets, etc.).


🧩 Example to understand

Imagine Kubernetes is a school 🏫:

The Principal is the kube-apiserver
The Teachers are the Controllers, Scheduler, etc.
The Students are the Pods

Now… every decision, every change, every student’s detail must be recorded somewhere, right?

That record book 📖 = etcd
Without etcd, the school (cluster) forgets who is in which class, what subjects exist, etc.


⚙️ What exactly etcd stores?

etcd stores all the cluster state, for example:

| Data Type              | Example                              |
| ---------------------- | ------------------------------------ |
| Nodes                  | Which worker nodes exist             |
| Pods                   | Which Pods are running, their status |
| ConfigMaps             | Configuration data                   |
| Secrets                | Passwords, tokens                    |
| Deployments / Services | App definitions                      |
| Cluster info           | Roles, namespaces, networking info   |


So if your Kubernetes cluster RESTARTS, it uses etcd to restore the last known state (what was running, where, etc.).


🏗️ Where does etcd run?

etcd runs inside the Control Plane (Master Node)
Usually as a Pod called etcd
The kube-apiserver communicates with etcd constantly.

🧭 Every time you use a command like:

kubectl get pods


Here’s what happens:


kubectl → talks to the kube-apiserver
apiserver → reads data from etcd
The result (pod list) comes back to you.


Node components
=============
kubelet --> agent running in every node. connects the nodes and master and makes sure containers are running inside pod.
kube-proxy --> networking rules how to send traffic to pods
Container runtime --> containerd, runc, etc. runs the containers


add-ons: adds capabilities to the cluster. vpc-cni, dns, metric server, etc.

cart -> catalogue

cart -> catalogue:8080

http:://catalogue-preview:8080/health --> success