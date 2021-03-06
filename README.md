# awx-ha-cluster

[AWX](https://github.com/ansible/awx) is an upstream project of Ansible Tower. Commercial Ansible Tower comes with clustering functionality out of the box. More likely the same functionality can be achieved in AWX by tweaking few file modifications and settings. Ideas from  official Ansible Tower installation playbook and sub-reddits.

## AWX configuration and deployment

### Install

```bash
ansible-playbook -i inventory/demo -e @vars/demo.yml -e task=setup awx.yml
ansible-playbook -i inventory/demo -e @vars/demo.yml -e task=run --tags postgres,rabbitmq,webhook awx.yml
ansible-playbook -i inventory/demo -e @vars/demo.yml -e task=run --tags awx --limit first_awx_node awx.yml
ansible-playbook -i inventory/demo -e @vars/demo.yml awx.yml
```

### Upgrade

```bash
ansible-playbook -i inventory/demo -e @vars/demo.yml -e task=setup --tags awx awx.yml
ansible-playbook -i inventory/demo -e @vars/demo.yml -e task=upgrade --tags awx awx.yml
ansible-playbook -i inventory/demo -e @vars/demo.yml --tags awx awx.yml
```

### Remove old Docker images

```bash
ansible -i inventory/demo all -a "docker rmi awx_web_img_id awx_task_img_id"
```
