# 📘 Kubernetes Resources – Complete Notes

Kubernetes resources are **objects** you define in YAML/JSON.  
They describe the **desired state** of your cluster.  
Kubernetes then makes the **actual state** match it (declarative model).

---

## 1. Workload Resources (Run Applications)

- **Pod** → Smallest unit, runs 1 or more containers.  
- **ReplicaSet** → Ensures a fixed number of Pods are always running.  
- **Deployment** → Manages ReplicaSets (easy rollout & rollback).  
- **StatefulSet** → Like Deployment, but Pods have stable IDs (for DBs, Kafka, etc.).  
- **DaemonSet** → Runs **1 Pod on every Node** (monitoring/logging agents).  
- **Job** → Runs a task once → then stops.  
- **CronJob** → Runs Jobs on a schedule (like Linux cron).  
- **ReplicationController** → Old way of managing Pods (replaced by ReplicaSet, but still exists).

---

## 2. Service Resources (Networking & Discovery)

- **Service** → Stable IP/Name to access Pods.  
  - **ClusterIP** → Internal only.  
  - **NodePort** → Expose app on Node’s port.  
  - **LoadBalancer** → Expose app to internet via cloud LB.  
- **Endpoint / EndpointSlice** → Store actual Pod IPs behind a Service (auto-managed).  
- **Ingress** → Routes external HTTP/HTTPS traffic to Services.  
- **NetworkPolicy** → Defines which Pods can talk to which Pods (firewall rules).

---

## 3. Config & Storage

- **ConfigMap** → Store non-secret config (key:value).  
- **Secret** → Store sensitive data (passwords, API keys).  
- **Volume** → Basic storage attached to Pod (ephemeral unless backed by PV).  
- **PersistentVolume (PV)** → Actual storage in cluster (disk, NFS, cloud).  
- **PersistentVolumeClaim (PVC)** → Pod’s request for storage.  
- **StorageClass** → Defines *how* PVs are provisioned dynamically.  

---

## 4. Security & Access Control (RBAC)

- **ServiceAccount** → Identity for Pods (for API access).  
- **Role** → Permissions inside a Namespace.  
- **ClusterRole** → Permissions across the whole cluster.  
- **RoleBinding** → Attach Role to user/service account.  
- **ClusterRoleBinding** → Attach ClusterRole to user/service account.  

---

## 5. Management & Organization

- **Namespace** → Logical separation (like folders).  
- **ResourceQuota** → Limit total CPU/memory/storage in a Namespace.  
- **LimitRange** → Define min/max CPU/memory per Pod/Container.  

---

## 6. Cluster-Level Resources (Good to Know)

- **Node** → Worker machine in the cluster.  
- **Event** → Auto-generated logs about what’s happening (Pod created, failed, scheduled, etc.).  

---

# 📝 Quick Memory Groups

1. **Workloads** → Pod, ReplicaSet, Deployment, StatefulSet, DaemonSet, Job, CronJob, ReplicationController  
2. **Networking** → Service, Ingress, Endpoint, NetworkPolicy  
3. **Data** → ConfigMap, Secret, Volume, PV, PVC, StorageClass  
4. **Security** → ServiceAccount, Role, ClusterRole, RoleBinding, ClusterRoleBinding  
5. **Management** → Namespace, ResourceQuota, LimitRange  
6. **Cluster Basics** → Node, Event  

---

# ⚡ Summary

- Run apps → *Pods, Deployments, StatefulSets, Jobs*  
- Connect apps → *Services, Ingress, NetworkPolicy*  
- Store data → *ConfigMap, Secret, PV/PVC, StorageClass*  
- Secure & control → *RBAC (Roles, Bindings, ServiceAccounts)*  
- Organize & limit → *Namespace, Quotas, LimitRange*  
- Cluster info → *Node, Events*  

---

✅ With this, you now have **all Kubernetes resources** clearly grouped for:
- **Learning concepts**  
- **Interview prep**  
- **Quick revision**
