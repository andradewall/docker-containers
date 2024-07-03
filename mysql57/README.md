# MySQL 5.7 Container

This container is for MySQL 5.7, which uses the Docker image [mysql:5.7.44](https://hub.docker.com/layers/library/mysql/5.7.44/images/sha256-dab0a802b44617303694fb17d166501de279c3031ddeb28c56ecf7fcab5ef0da?context=explore)

## Installation

1. Manually create the network for MySQL:

```bash
docker network create mysql57_net
```

2. Create and start running the container on detached mode:

```bash
docker compose up -d
```
