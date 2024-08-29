# 🐘 PostgreSQL

This container is for [PostgreSQL](https://www.postgresql.org/), which uses the Docker image [postgres](https://hub.docker.com/_/postgres)

## Installation

1. Manually create the network for PostgreSQL:

```bash
docker network create --subnet=10.5.0.0./16 --gateway=10.5.0.1 postgres_net
```

2. Create and start running the container on detached mode:

```bash
docker compose up -d
```

> [!NOTE]
> This container will receive the IP `10.5.0.2`
