---
description: >-
  Use caddy as reverser proxy with https included for docker container in single
  host
---

# Docker-compose caddy as reverse proxy

**Usage:**

```
docker network create caddy
docker compose -f caddy-compose.yml up -d
docker compose -f docker-compose.yml up -d
```

* Make sure port 80, 443 is open and DNS config of domain map to ip of server

**caddy-compose.yml**

```yaml

version: "3.7"
services:
  caddy:
    image: lucaslorentz/caddy-docker-proxy:2.8-alpine
    ports:
      - 80:80
      - 443:443
    environment:
      - CADDY_INGRESS_NETWORKS=caddy
    networks:
      - caddy
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - caddy_data:/data
    restart: unless-stopped

networks:
  caddy:
    external: true

volumes:
  caddy_data: {}

```

**docker-compose.yml**

```yaml
version: '3.3'

services:
  # https://mockoon.com
  mockoon:
    image: mockoon/cli:latest
    restart: unless-stopped
    networks:
      - caddy
      - frontend
      - backend
    labels:
      caddy: mockoon.dummydomain.com
      caddy.reverse_proxy: '{{upstreams 3000}}'
    volumes:
      - ./dev/mockoon/data.json:/data
    command: -d data -p 3000


networks:
  caddy:
    external: true
```

