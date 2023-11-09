---
description: Truncate all docker logs in an instance to free up disk space
---

# Truncate docker log

```
sudo truncate -s 0 /var/lib/docker/containers/*/*-json.log
```

\#docker #docker-container #docker-log #script #devops #maintain #system-operation
