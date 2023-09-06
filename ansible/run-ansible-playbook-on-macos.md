---
description: https://github.com/ansible/ansible/issues/76322
---

# Run Ansible Playbook on MacOS

[https://github.com/ansible/ansible/issues/76322](https://github.com/ansible/ansible/issues/76322)

```

export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
ansible-playbook -i hosts.ini your_playbook.yml

```
