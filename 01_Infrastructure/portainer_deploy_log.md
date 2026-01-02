## Project Documentation: Infrastructure Foundation (Project 1)

### 📄 Document: `portainer_deploy_log.md`

**Project Name:** Foundational Docker Management (Portainer CE)

**Status:** Operational

**Date:** 2026-01-02

**Host OS:** Windows 11 (Unactivated) using WSL2 (Ubuntu 22.04)

#### 1. Objective

To move away from resource-heavy standalone deployments and establish a **GUI-based orchestration layer**. This allows for real-time monitoring of CPU/RAM and simplified management of persistent data volumes.

#### 2. Deployment Commands

The following commands were executed in PowerShell to initialize the environment:

**Step A: Create Persistent Storage**
This ensures that your admin settings and dashboard configurations survive container restarts or updates.

```powershell
docker volume create portainer_data

```

**Step B: Deploy the Management Container**
This command pulls the latest Community Edition image and binds it to the Docker engine.

```powershell
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

```

#### 3. Configuration Details

* **Web UI Access:** `https://localhost:9443`
* **Authentication:** Admin account initialized with manual password entry.
* **Environment:** Connected via **Local Unix Socket** (`/var/run/docker.sock`), giving Portainer "Full Control" over the local Docker engine.

---




