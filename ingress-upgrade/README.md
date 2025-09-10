# Ingress-NGINX Upgrade Guide (Helm)

This guide explains how to **upgrade an existing Ingress-NGINX installation** on Kubernetes using Helm.

---

## ✅ Prerequisites

- Kubernetes cluster (v1.20+ recommended)
- `kubectl` and `helm` installed and configured
- Existing Ingress-NGINX deployment via Helm (e.g., `ingress-nginx` release)
- Access to Helm chart repository

---

## 📥 Check Current Installation

1. List Helm releases
   
```
helm list -A
```

Look for your Ingress-NGINX release name (e.g., ingress-nginx) and namespace.

1. Check current version

```
helm status ingress-nginx -n ingress-nginx
kubectl get deployment ingress-nginx-controller -n ingress-nginx -o yaml | grep image:
```

## 🔄 Upgrade Using Helm

1. Update Helm repo

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

2. Preview upgrade

helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --dry-run

The --dry-run flag lets you see changes without applying them.

3. Perform the upgrade

helm upgrade ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --reuse-values

--reuse-values ensures your existing configuration is preserved.

If you want to override specific values, you can use --set key=value or -f values.yaml.

## 💾 Verify the Upgrade

1. Check deployment rollout status:

kubectl rollout status deployment/ingress-nginx-controller -n ingress-nginx

2. Confirm pods are updated:

kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx

1. Validate Ingress functionality:

kubectl get ingress -A

Test by accessing your services through the Ingress.