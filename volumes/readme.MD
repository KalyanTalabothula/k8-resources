Ok 👌 let’s slow down right at that point:

👉 You said “That path is linked to → K8s Volume (persistent-storage).”
This is the tricky part, so let me make it very clear with an example.

1. Container path (mountPath)

In your Pod spec:

volumeMounts:
- name: persistent-storage
  mountPath: /usr/share/nginx/html


This means:
Inside the nginx container, the folder /usr/share/nginx/html is not just a normal folder anymore.
It is connected to something Kubernetes calls a Volume.

2. Volume (volumes section)
volumes:
- name: persistent-storage
  persistentVolumeClaim:
    claimName: ebs-static


Here you are saying:
“This volume (persistent-storage) is not temporary, it comes from a PVC called ebs-static.”

So Kubernetes takes the volumeMounts.name (persistent-storage) and matches it with the volumes.name (persistent-storage).

That’s the link.

🔗 How linking works

Think of it like a plug and socket:

mountPath (container) = where to plug inside container (like a USB port).

volumes (Pod spec) = what to plug in (like a USB drive).

So:

The container only knows the path: /usr/share/nginx/html.

The Pod spec tells Kubernetes: “The thing connected here is not empty, it’s actually a PVC (ebs-static) → which is an EBS disk.”

3. Simple analogy

Imagine you have a laptop (container).

You say: “At this USB port (mountPath), I want storage.”

Kubernetes says: “Okay, I’ll plug in this external hard drive (PVC → PV → EBS).”

Now when you save files in that folder, they go directly into the external hard drive.

✅ Final flow
Container path (/usr/share/nginx/html)
        ⬇ linked to
K8s Volume (persistent-storage)
        ⬇ connected by
PVC (ebs-static)
        ⬇ backed by
AWS EBS disk (real storage)


So when I say “That path is linked to K8s Volume (persistent-storage)”, it means:

/usr/share/nginx/html is not just an empty folder → it is connected to a Kubernetes Volume, which is further connected to real storage (EBS).