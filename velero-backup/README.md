# Velero Backup Guide

This guide explains how to install, configure, and use Velero to back up Kubernetes clusters.

---

## ✅ Prerequisites

- A Kubernetes cluster (v1.20+)
- `kubectl` aand `helm` installed and configured
- A HCP S3 object storage

---

## 📥 Installation

1. Add the Velero Helm repo

   ```
   helm repo add vmware-tanzu https://vmware-tanzu.github.io/helm-charts
   helm repo update
   ```
   
2. Install Velero

```
helm install velero vmware-tanzu/velero \
  --namespace velero \
  --create-namespace \
  --set configuration.provider=aws \
  --set-file credentials.secretContents.cloud=./credentials-velero \
  --set configuration.backupStorageLocation.name=default \
  --set configuration.backupStorageLocation.bucket=<YOUR_BUCKET> \
  --set configuration.backupStorageLocation.config.region=<REGION>
  ```

3. Check that Velero pods are running

```
kubectl get pods -n velero
```

## 💾 Creating a Backup

1. To back up a specific namespace

```
velero backup create my-backup --include-namespaces my-namespace
```

2. To back up the entire cluster

```
velero backup create cluster-backup
```

3. Verify backups

```
velero backup get
```

## 📅 Scheduling Backups

1. To create a daily backup schedule at 2 AM

```
velero schedule create daily-backup \
  --schedule="0 2 * * *" \
  --include-namespaces my-namespace
```

2. List schedules

```
velero schedule get
```

## 🔄 Restoring Backups

1. Restore from a backup

```
velero restore create --from-backup my-backup
```

2. List restores

```
velero restore get
```