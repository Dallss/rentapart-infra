# RentApart Infra

Infrastructure repository for deploying the RentApart platform using Docker Compose and a self-hosted GitHub Actions runner.

## Purpose

This repository is responsible for:

- Managing the deployment stack
- Running services through Docker Compose
- Pulling latest images from GitHub Container Registry (GHCR)
- Hosting deployment workflows
- Running the self-hosted GitHub Actions runner on the VM

---

## Services

Current microservices powering the RentApart platform:

- [`rentapart`](https://github.com/Dallss/rentapart) — backend service responsible for API, authentication, and business logic

- [`rent-apart`](https://github.com/Dallss/rent-apart) — frontend application serving the user interface and client-side experience
  

Each service repository:

1. Builds a Docker image
2. Pushes the image to GHCR
3. Triggers this infra repository to deploy

---

## Deployment Flow

```text
Push to app repo
      ↓
Build Docker image
      ↓
Push image to GHCR
      ↓
Trigger infra deploy workflow
      ↓
Self-hosted runner on VM executes deployment
      ↓
docker compose pull
docker compose up -d --remove-orphans
```

---


## Notes

- Uses Docker Compose for orchestration
- Uses GHCR for container registry
- Uses a self-hosted GitHub Actions runner for deployments
- App repositories remain separate from infrastructure configuration
