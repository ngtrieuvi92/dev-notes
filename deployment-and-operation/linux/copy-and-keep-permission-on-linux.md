---
description: How do I copy a folder keeping owners and permissions intact?
---

# Copy and keep permission on linux

```bash
sudo cp -rp /home/my_home /media/backup/my_home
```

```bash
From cp manpage:

 -p     same as --preserve=mode,ownership,timestamps

 --preserve[=ATTR_LIST]
          preserve the specified attributes (default: mode,ownership,timestamps),
          if possible additional attributes: context, links, xattr, all
```
