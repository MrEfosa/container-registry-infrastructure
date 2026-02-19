# Local Setup  
## Running Nexus as a Private Docker Registry (Local Machine)

---

## Prerequisites

- Docker installed
- Docker running
- At least 2GB RAM available for Nexus

Verify Docker:

```bash
docker --version
```

---

## Step 1: Create a Docker Volume

Nexus requires persistent storage.

```bash
docker volume create nexus-data
```

Verify:

```bash
docker volume ls
```

---

## Step 2: Run Nexus Container

```bash
docker run -d \
  --name nexus \
  -p 8081:8081 \
  -p 8083:8083 \
  -v nexus-data:/nexus-data \
  sonatype/nexus3
```
### With Docker Compose

```bash
docker-compose -f docker-compose.yaml
```

Check container:

```bash
docker ps
```

---

## Step 3: Access Nexus UI

Open browser:

```
http://localhost:8081
```

Default username:
```
admin
```

Retrieve initial password:

```bash
docker exec nexus cat /nexus-data/admin.password
```

---

## Step 4: Create Docker Hosted Repository

Inside Nexus UI:

1. Go to Settings → Repositories
2. Create repository
3. Select **Docker (hosted)**
4. Name it (e.g., docker-hosted)
5. Set HTTP port to 8083
6. Save

---

## Step 5: Configure Docker for HTTP Registry

Edit Docker daemon configuration.

On Linux:

```bash
sudo nano /etc/docker/daemon.json
```

Add:

```json
{
  "insecure-registries": ["localhost:8083"]
}
```

Restart Docker:

```bash
sudo systemctl restart docker
```

---

## Step 6: Tag and Push Image

Tag image:

```bash
docker tag my-app:1.0 localhost:8083/my-app:1.0
```

Login:

```bash
docker login localhost:8083
```

Push:

```bash
docker push localhost:8083/my-app:1.0
```

Verify inside Nexus UI.

---

## Local Setup Complete

