# 🎨 Color App – Kubernetes Demo

Simple Kubernetes project to deploy a Color App using:

- Namespace
- ConfigMap
- Secret
- Deployment (3 replicas)
- Service (ClusterIP)
- Ingress (Traefik)

---

## 📦 Architecture

Namespace: color-app  
Inside it:

- ConfigMap → defines COLOR=blue
- Secret → stores PASSWORD (Base64)
- Deployment → 3 Pods running minaamin/color-app:v1
- Service → exposes app internally on port 80
- Ingress → routes colorapp.local to the service

---

## 🚀 Deploy the App

Apply the manifest file:

```bash
kubectl apply -f color-app.yaml
```

Check resources:

```bash
kubectl get all -n color-app
```

---

## 🌐 Access the Application (Local Cluster)

If you are using k3s or any local Kubernetes cluster:

1. Edit your hosts file:

Linux / Mac:
```bash
sudo nano /etc/hosts
```

Windows:
```
C:\Windows\System32\drivers\etc\hosts
```

Add:

```
<MASTER-IP>   colorapp.local
```

2. Open in browser:

```
http://colorapp.local
```

---

## 🔐 Environment Variables

The container receives:

- COLOR → from ConfigMap
- password → from Secret

To change the color:

```bash
kubectl edit configmap color-config -n color-app
```

Then restart pods if needed:

```bash
kubectl rollout restart deployment color-deployment -n color-app
```

---

## 📌 Requirements

- Kubernetes Cluster
- kubectl configured
- Traefik Ingress Controller installed

---

## 📝 Notes

- Secret is Base64 encoded (not encrypted).
- Service type is ClusterIP (internal).
- Ingress is configured with ingressClassName: traefik.
- Deployment has resource requests and limits configured.