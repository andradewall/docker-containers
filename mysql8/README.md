# 🐬 MySQL 8.4

[MySQL 8.4](https://www.mysql.com/) container based on [mysql:lts](https://hub.docker.com/layers/library/mysql/lts/images/sha256-12f800accdf4aacff75dc1b00a41b17be628240e9f6f8cb355a185df4f86e151?context=explore) image.

## Installation

1. Manually create the network for MySQL:

```bash
docker network create --subnet=10.7.0.0/16 --gateway=10.7.0.1 mysql8_net
```

2. Create and start running the container on detached mode:

```bash
docker compose up -d
```

> [!NOTE]
> This container will receive the IP `10.7.0.2`
