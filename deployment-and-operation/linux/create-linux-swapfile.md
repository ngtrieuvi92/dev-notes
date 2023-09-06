---
description: Create linux swap
---

# Create linux Swapfile

```
sudo fallocate -l 4G /swapfile && \
sudo chmod 600 /swapfile && \
sudo mkswap /swapfile && \
sudo swapon /swapfile && \
sudo swapon -s && \
sudo cp /etc/fstab /etc/fstab.bak && \
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
