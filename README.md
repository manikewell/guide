# Kubernetes Guides

This repository contains step-by-step guides and documentation for common Kubernetes operations and tools.  
Each guide is self-contained inside its own folder with a `README.md` and supporting images.

---

## 📚 Available Guides

- [Velero Backup](./velero-backup/README.md) – How to set up and schedule backups with Velero
- [Ingress-NGINX Upgrade](./ingress-nginx-upgrade/README.md) – How to upgrade Ingress-NGINX using Helm

---

## 🗂 Repository Structure

```text
guides/
├── README.md                  # Overview and index of all guides
├── velero-backup/             # Velero backup guide
│   ├── README.md
│   └── images/
│       └── .gitkeep
└── ingress-nginx-upgrade/     # Ingress upgrade guide
    ├── README.md
    └── images/
        └── .gitkeep
```

## 🔧 Contributing

To add a new guide:

1. Create a new subfolder under `guides/` in **kebab-case** (e.g., `my-new-guide`).
2. Add a `README.md` with step-by-step instructions.
3. Add supporting images in an `images/` subfolder.
4. Update this root `README.md` to link to your new guide.

---
