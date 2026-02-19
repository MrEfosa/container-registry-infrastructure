# Cloud Deployment Guide  
## Deploying Nexus on a DigitalOcean Droplet

---

## Prerequisites

- DigitalOcean account
- Ubuntu droplet (recommended: 2GB RAM minimum)
- SSH access
- Docker installed on droplet

---

## Step 1: SSH into Server

```bash
ssh root@your_server_ip
```

---

## Step 2: Install Docker (if not installed)

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

Verify:

```bash
docker --version
```

---

## Step 3: Create Volume

```bash
docker volume create nexus-data
```

---

## Step 4: Run Nexus

```bash
docker run -d \
  --name nexus \
  -p 8081:8081 \
  -p 8083:8083 \
  -v nexus-data:/nexus-data \
  sonatype/nexus3
```
### With Docker-compose

```bash
docker-compose -f docker-compose.yaml

```

## Step 5: Open Firewall Ports

Allow ports:

- 22 (SSH)
- 8081 (Nexus UI)
- 8083 (Docker registry)

On Ubuntu:

```bash
sudo ufw allow 8081
sudo ufw allow 8083
sudo ufw enable
```

Also allow these ports in DigitalOcean firewall settings.

---

## Step 6: Access Nexus

Open:

```
http://your_server_ip:8081
```

Retrieve admin password:

```bash
docker exec nexus cat /nexus-data/admin.password
```

---

## Step 7: Push Image from Local Machine

On your local computer:

Edit Docker daemon.json:

```json
{
  "insecure-registries": ["your_server_ip:8083"]
}
```

Restart Docker.

Tag image:

```bash
docker tag my-app:1.0 your_server_ip:8083/my-app:1.0
```

Login:

```bash
docker login your_server_ip:8083
```

Push:

```bash
docker push your_server_ip:8083/my-app:1.0
```

---

## Cloud Deployment Complete

