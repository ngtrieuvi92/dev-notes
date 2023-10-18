# Nginx - 504 Gateway Timeout error using Nginx as Proxy

**Nginx as Proxy** for  Web server, we can to try to fix the 504 Gateway Timeout error:

**Add these variables to `nginx.conf` file:**

```
  proxy_connect_timeout       600;
  proxy_send_timeout          600;
  proxy_read_timeout          600;
  send_timeout                600;
```

or add it to server block

```
server {
    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_http_version 1.1;
        proxy_set_header Connection "";
        proxy_pass http://localhost:5000;
        proxy_connect_timeout       600;
        proxy_send_timeout          600;
        proxy_read_timeout          600;
        send_timeout                600;
    }
}
```

**Then restart nginx:**

```
service nginx reload
```
