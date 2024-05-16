# Download file from server via nginx docker

Crete struct folder like this:&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2024-05-16 at 15.45.08@2x.png" alt=""><figcaption></figcaption></figure>

1. Put all your download files into **files**  folder

<figure><img src="../../.gitbook/assets/CleanShot 2024-05-16 at 15.42.55@2x.png" alt=""><figcaption></figcaption></figure>



1. Create file conf/dowload.conf

```
server {
  listen 80;
  server_name _;
  # serve the static files on port 80
  location /downloads/ {
    alias /files/;
  }
}
```

3. Create docker compose file:

```
version: '3'

services:
  nginx:
    image: nginx:latest
    volumes:
      - ./files:/files
      - ./conf:/etc/nginx/conf.d
    ports:
      - "8080:80"
```



4. Start docker container

```
docker compose up -d
```

5. Download files

```
curl http://your_ip:8080/downloads/files.sql.gz
```

6. Shutdown container after download

```
docker compose down
```
