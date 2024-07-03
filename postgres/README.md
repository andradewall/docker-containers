
# PostgreSQL Container

This container is for PostgreSQL, which uses the Docker image `postgres`

## Installation

1. Manually create the network for PostgreSQL:

```bash
docker network create postgres
```

2. Create and start running the container on detached mode:

```bash
docker compose up -d
```
