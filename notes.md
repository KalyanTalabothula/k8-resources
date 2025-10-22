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


| Concept    | Terraform                         | Kubernetes                      |
| ---------- | --------------------------------- | ------------------------------- |
| Storage    | `.tfstate` file (local or remote) | `etcd` database                 |
| Managed by | Terraform tool                    | kube-apiserver                  |
| Type       | File-based JSON                   | Distributed key-value store     |
| Usage      | Tracks cloud infra state          | Tracks cluster & workload state |
| Backup     | Copy `.tfstate`                   | `etcdctl snapshot save`         |

So yes — conceptually same idea (both store state),
but technically different systems (file vs. database).

| Component                   | Function                                                                    |
| --------------------------- | --------------------------------------------------------------------------- |
| **etcd**                    | Database → stores all cluster state                                         |
| **kube-apiserver**          | Gateway → talks to etcd and other control plane parts                       |
| **kube-controller-manager** | Ensures cluster state matches desired state (e.g., creates pods if missing) |
| **kube-scheduler**          | Decides on which node each pod should run                                   |
| **kubelet (on each node)**  | Runs pods and reports back to API server                                    |

👉 All these components are part of the control plane,
and they all depend on etcd to store and read data.


📊 Flow example

You create a Deployment → API Server receives it.
API Server saves it to etcd.
Controller Manager reads from etcd → creates ReplicaSets, Pods, etc.
Scheduler picks which node → updates etcd.
Kubelet runs Pod → updates status in etcd.
Everything → saved and synced in etcd ✅

| Component                   | Simple meaning    | Job                                                       |
| --------------------------- | ----------------- | --------------------------------------------------------- |
| **etcd**                    | Memory / Database | Stores everything about cluster (Pods, Nodes, Secrets...) |
| **kube-apiserver**          | Receptionist      | First contact point — all communication goes through it   |
| **kube-controller-manager** | Manager           | Watches etcd, fixes things automatically                  |
| **kube-scheduler**          | Planner           | Decides which node runs each Pod                          |


All these 4 together = Control Plane. ✅

🧠 Step 2: What is the “Controller Manager”?

The Controller Manager is just one part inside the control plane.
Its job: make sure the cluster’s actual state = desired state.

Example 👇
You said “I want 3 Pods of Nginx” (in Deployment YAML).

etcd stores this info.

Controller Manager checks etcd:

“Hmm, only 2 Pods are running, but 3 are needed.”

It creates 1 more Pod to fix it.

💬 So the Controller Manager reads data from etcd,
but it doesn’t store anything itself — it just acts on data.



🧠 Step 3: What is “etcd”?

etcd = Database / Memory for the control plane.

It doesn’t make decisions.
It just stores everything:

Pod info
Deployment info
ConfigMaps
Secrets
Node info

Whenever anything changes in the cluster — it’s saved to etcd.

Node components
=============
kubelet --> agent running in every node. connects the nodes and master and makes sure containers are running inside pod.
kube-proxy --> networking rules how to send traffic to pods
Container runtime --> containerd, runc, etc. runs the containers


add-ons: adds capabilities to the cluster. vpc-cni, dns, metric server, etc.

cart -> catalogue

cart -> catalogue:8080

http:://catalogue-preview:8080/health --> success

| Add-on                    | Purpose / What it does                                                |
| ------------------------- | --------------------------------------------------------------------- |
| **CoreDNS**               | Provides DNS (name → IP) inside cluster (so pods can find each other) |
| **kube-proxy**            | Handles network routing inside the cluster                            |
| **Dashboard**             | Web UI for Kubernetes                                                 |
| **Metrics Server**        | Collects resource metrics (CPU, memory) for autoscaling               |
| **Ingress Controller**    | Manages external access (like load balancer)                          |
| **Network Add-ons (CNI)** | Provide pod-to-pod networking (e.g., Calico, Flannel, Weave)          |
| **Storage Add-ons (CSI)** | Manage storage volumes (e.g., EBS, Ceph, NFS)                         |
| **Monitoring tools**      | Prometheus, Grafana — monitor your cluster                            |
| **Logging tools**         | Fluentd, Loki — collect and view logs                                 |
