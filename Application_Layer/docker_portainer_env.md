# Phase 2: Application Layer Deployment

## Docker Installation
Installed the Docker engine using the official automated convenience script.


# Download and execute install script
```
curl -fsSL [https://get.docker.com](https://get.docker.com) -o get-docker.sh
sudo sh get-docker.sh
```


---

Post-Installation Steps
Resolved initial permission issues where docker run failed due to lack of API socket access.



# Manage user permissions
```
sudo usermod -aG docker $USER
```
```
newgrp docker
```
Management Dashboard (Portainer)
Deployed Portainer CE for container orchestration.

---
```
docker volume create portainer_data
```
```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data portainer/portainer-ce:latest
```

---
