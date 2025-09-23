# Kubernetes Resource Limiting

A simple guide to understand **Resource Limiting** in Kubernetes.  
Includes **theory + example YAML + container vs VM comparison**.

---

## 🔹 What is Resource Limiting?

Every Pod (or container) in Kubernetes needs **CPU** and **Memory** to run.  

If we don’t control it → one container can consume all resources of the Node → crash or slow down other apps.

**Resource Limiting = putting boundaries (limits) on how much CPU/Memory a container can use.**

---

## 🔹 Two Key Terms

**Requests 🏷️**  
- Minimum guaranteed resources a container will get.  
- Kubernetes scheduler uses this to decide **which Node can run the Pod**.  

**Limits 🚧**  
- Maximum resources a container can use.  
- If container exceeds limit:  
  - CPU → throttled (slowed down)  
  - Memory → Pod gets killed (OOM – Out of Memory)

---

## 🔹 Example YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
  - name: app
    image: nginx
    resources:
      requests:
        cpu: "200m"      # 0.2 CPU
        memory: "256Mi"  # 256 MB RAM
      limits:
        cpu: "500m"      # 0.5 CPU
        memory: "512Mi"  # 512 MB RAM
