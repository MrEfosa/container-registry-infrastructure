# Private Docker Registry with Nexus  
### Local & Cloud Deployment | DevOps Infrastructure Project

---

## Overview

This project demonstrates the design and deployment of a **private Docker registry** using Nexus Repository Manager.

The implementation was completed in two phases:

1. **Local Deployment** using Docker  
2. **Cloud Deployment** on a remote Linux server (DigitalOcean droplet)

The goal was to understand container persistence, registry configuration, image distribution workflows, and infrastructure deployment from a practical DevOps perspective.

---

## Architecture

### Local Environment

```
Docker Client
     ↓
Nexus Container
     ↓
Docker Volume (Persistent Storage)
```

### Cloud Environment

```
Local Docker Client
        ↓
      Internet
        ↓
Cloud Server (Ubuntu)
        ↓
Nexus Container
        ↓
Persistent Volume
```

Nexus functions as a **self-hosted Docker registry**, similar to Docker Hub but fully controlled within private infrastructure.

---

## Core Features Implemented

- Containerized Nexus deployment
- Persistent storage using Docker volumes
- Docker hosted repository configuration
- Image tagging and push workflow
- Registry authentication
- Remote server deployment via SSH
- Firewall and port exposure management
- Systematic troubleshooting and debugging

---

## Repository Structure

```
container-registry-infrastructure/
│
├── docker-compose.yml
├── README.md
├── local-setup.md
├── cloud-deployment.md
├── troubleshooting.md
├── .gitignore

```
---

## Key Engineering Concepts Demonstrated

- Containers are ephemeral; volumes preserve state  
- Image tagging determines registry destination  
- HTTP registries require Docker daemon configuration  
- Remote deployment introduces firewall and networking considerations  
- Infrastructure debugging requires layer-by-layer validation  

---

## Security Considerations

For learning purposes, the registry was configured over HTTP.  
In a production environment, improvements would include:

- HTTPS with SSL certificates
- Reverse proxy configuration (e.g., Nginx)
- Access control hardening
- CI/CD automation for image publishing

---

## What This Project Demonstrates

This project reflects practical understanding of:

- Container infrastructure design  
- Artifact management systems  
- Registry architecture  
- Cloud-based deployment workflows  
- Infrastructure troubleshooting  

---

## Outcome

Successfully built and deployed a fully functional private Docker registry both locally and in the cloud, reinforcing foundational DevOps engineering principles and real-world deployment practices.

---

## Author

Onyekaozuru Tochukwu David

