---
description: Add user to sudo group and allow to use sudo without password
---

# Linux - add user to sudo group

```bash

# Create new user
adduser your_user

# Add to sudo group
sudo usermod -aG sudo your_user

# (optional) Allow to use sudo without password
echo 'your_user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
```
