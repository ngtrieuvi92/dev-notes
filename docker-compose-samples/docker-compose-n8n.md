# docker-compose - n8n

```
version: "3"
services:

  n8n:
    image: n8nio/n8n
    restart: always
    ports:
      - "5678:443"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER
      - N8N_BASIC_AUTH_PASSWORD
      - N8N_HOST=${SUBDOMAIN}.${DOMAIN_NAME}
      - N8N_PORT=443
      - N8N_PROTOCOL=https
      - NODE_ENV=production
      - WEBHOOK_URL=https://${SUBDOMAIN}.${DOMAIN_NAME}/
      - GENERIC_TIMEZONE=${GENERIC_TIMEZONE}
    volumes:
      - ${DATA_FOLDER}/.n8n:/home/node/.n8n
  nodedb:
    image: mysql:8.0.32
    container_name: nodedb
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_DATABASE: nodedb
      MYSQL_ROOT_PASSWORD: you_root_pass_work
    volumes:
      - ${NODEDB_DATA_FOLDER}:/var/lib/mysql
```
