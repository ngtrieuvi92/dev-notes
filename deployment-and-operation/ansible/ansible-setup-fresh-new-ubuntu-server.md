---
description: >-
  # Run on Mac OS: (https://github.com/ansible/ansible/issues/76322) # export
  OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES # ansible-playbook -i hosts.ini
  setup-new-instance-playbook.yml
---

# Ansible - Setup fresh new ubuntu server

```yaml
#################################################
# SMT Playbooks: Initial Server Setup
#################################################

# Run on Mac OS: (https://github.com/ansible/ansible/issues/76322)
# export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
# ansible-playbook -i hosts.ini setup-new-instance-playbook.yml
---
- name: Setup new Ubuntu Server
  hosts: aws_node_01
  become: true
  roles:
    - ngtrieuvi92.setup_ubuntu_sever
    - ansible-node-exporter
    - role: geerlingguy.docker
      become: true
  become_user: "{{target_user}}"

  vars:
    ansible_user: ubuntu
    ansible_ssh_private_key_file: ~/.ssh/main_private_key.pem
    target_user: nimbus
    ssh_public_key_paths:
      - ~/.ssh/id_rds.pub
    # control docker install
    docker_users:
      - "{{target_user}}"
    docker_install_compose_plugin: true
    docker_compose_package: docker-compose-plugin
    docker_compose_package_state: present
    docker_install_compose: false

```
