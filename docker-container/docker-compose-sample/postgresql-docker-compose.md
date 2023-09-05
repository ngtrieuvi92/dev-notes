---
description: docker-compose-postgres.yml
---

# postgresql docker compose

```
version: '3.8'
services:
  db:
    image: postgres:14.1-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
volumes:
  db:
    driver: local
```

* [https://hub.docker.com/\_/postgres](https://hub.docker.com/\_/postgres)
* [https://geshan.com.np/blog/2021/12/docker-postgres/](https://geshan.com.np/blog/2021/12/docker-postgres/)
