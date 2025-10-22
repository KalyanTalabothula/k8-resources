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

Node components
=============
kubelet --> agent running in every node. connects the nodes and master and makes sure containers are running inside pod.
kube-proxy --> networking rules how to send traffic to pods
Container runtime --> containerd, runc, etc. runs the containers


add-ons: adds capabilities to the cluster. vpc-cni, dns, metric server, etc.

cart -> catalogue

cart -> catalogue:8080

http:://catalogue-preview:8080/health --> success