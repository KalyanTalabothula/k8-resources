# 🚀 Kubernetes Resources – Easy Notes with Icons

Kubernetes resources are **objects** you define in YAML/JSON.  
They describe the **desired state** of your cluster.  
Kubernetes makes the **actual state** match it (declarative model).

---

## 1. 🏗️ Workload Resources (Run Applications)

- 🟦 **Pod** → Smallest unit, runs 1 or more containers.  
- ♻️ **ReplicaSet** → Ensures a fixed number of Pods.  
- 📦 **Deployment** → Manages ReplicaSets (easy rollout & rollback).  
- 🏷️ **StatefulSet** → Like Deployment, but Pods keep stable IDs (DBs, Kafka).  
- 🌀 **DaemonSet** → Runs **1 Pod per Node** (e.g., logging, monitoring).  
- 🎯 **Job** → Runs a task once → then stops.  
- ⏰ **CronJob** → Runs Jobs on a schedule (like Linux cron).  
- 📜 **ReplicationController** → Old controller (replaced by ReplicaSet).

---

## 2. 🌐 Service & Networking Resources

- 🌐 **Service** → Stable IP/Name for Pods.  
  - 🟩 **ClusterIP** → Internal only.  
  - 🟧 **NodePort** → Exposes app on Node’s port.  
  - 🟦 **LoadBalancer** → Exposes app externally via cloud LB.  
- 🧩 **Endpoint / EndpointSlice** → Actual Pod IPs behind a Service (auto-managed).  
- 🚪 **Ingress** → Routes external HTTP/HTTPS traffic to Services.  
- 🔒 **NetworkPolicy** → Rules for Pod-to-Pod communication (firewall).

---

## 3. 💾 Config & Storage Resources

- 🗂️ **ConfigMap** → Store non-secret configs (key:value).  
- 🔑 **Secret** → Store sensitive data (passwords, API keys).  
- 📂 **Volume** → Basic Pod-attached storage (ephemeral).  
- 💾 **PersistentVolume (PV)** → Actual cluster storage (disk, NFS, cloud).  
- 📥 **PersistentVolumeClaim (PVC)** → Pod’s request for PV storage.  
- ⚙️ **StorageClass** → Defines *how* PVs are provisioned dynamically.  

---

## 4. 🔐 Security & Access Control (RBAC)

- 🆔 **ServiceAccount** → Identity for Pods (to access API).  
- 📝 **Role** → Permissions in a Namespace.  
- 🌍 **ClusterRole** → Permissions across the whole cluster.  
- 🔗 **RoleBinding** → Attach Role → User/ServiceAccount.  
- 🔗🌍 **ClusterRoleBinding** → Attach ClusterRole → User/ServiceAccount.  

---

## 5. 🗄️ Management & Organization

- 📁 **Namespace** → Logical separation (like folders).  
- 📊 **ResourceQuota** → Limit total CPU/memory/storage in a Namespace.  
- 📏 **LimitRange** → Set min/max CPU/memory per Pod/Container.  

---

## 6. ⚙️ Cluster-Level Resources (Good to Know)

- 🖥️ **Node** → Worker machine in cluster.  
- 📢 **Event** → Auto-logs about what’s happening (Pod created, failed, scheduled, etc.).  

---

# 📝 Quick Memory Groups

1. **Workloads** → 🟦 Pod, ♻️ ReplicaSet, 📦 Deployment, 🏷️ StatefulSet, 🌀 DaemonSet, 🎯 Job, ⏰ CronJob, 📜 ReplicationController  
2. **Networking** → 🌐 Service, 🚪 Ingress, 🧩 Endpoints, 🔒 NetworkPolicy  
3. **Data** → 🗂️ ConfigMap, 🔑 Secret, 📂 Volume, 💾 PV, 📥 PVC, ⚙️ StorageClass  
4. **Security** → 🆔 ServiceAccount, 📝 Role, 🌍 ClusterRole, 🔗 RoleBinding, 🔗🌍 ClusterRoleBinding  
5. **Management** → 📁 Namespace, 📊 ResourceQuota, 📏 LimitRange  
6. **Cluster Basics** → 🖥️ Node, 📢 Event  

---

# 📊 Visual Flow (Big Picture)

```mermaid
flowchart LR
    User([👤 User]) --> Ingress[🚪 Ingress]
    Ingress --> Service[🌐 Service]
    Service --> Pods[🟦 Pods]
    Pods --> PVC[📥 PVC]
    PVC --> PV[💾 PV]
