## 📂 Phase 7: Application Layer Hardening

**File Path:** `/IT-Projects/02_Application_Layer/docker_rootless_migration.md`

### 📋 Overview

Transitioned the Docker engine from a system-wide "Rootful" installation to a "Rootless" configuration. This move implements the **Principle of Least Privilege**, ensuring that the Docker daemon and its containers run within a non-privileged user namespace.

### 🛠️ Execution Steps

1. **System Decommissioning**: Fully purged the `docker-ce` and `containerd.io` packages and manually removed persistent systemd units (`docker.service`, `docker.socket`) to prevent binary conflicts during migration.
2. **Security Policy Exception**: Configured a custom **AppArmor profile** for `rootlesskit` to allow unprivileged user namespace creation on Ubuntu 24.04.
3. **User-Space Installation**: Deployed the rootless engine using the specialized setup script, isolating all Docker data to `/home/adminuser/.local/share/docker`.
4. **Environment Mapping**: Updated `.bashrc` to export the local binary path and the user-specific socket path.

### 🔍 Technical Validation

| Metric | Expected Result | Actual Result |
| --- | --- | --- |
| **Daemon Owner** | `adminuser` (UID 1000) | **Verified** |
| **Security Mode** | `rootless` | **Verified** |
| **Service Context** | `systemctl --user` | **Verified** |
| **Socket Path** | `/run/user/1000/docker.sock` | **Verified** |

---

