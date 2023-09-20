RabbitMQ Ansible Role
=========

Install RabbitMQ, clustering, enable plugins, set users and policy for it with HAProxy & KeepAliveD for setup redundant service.

Requirements
------------

Use [RabbitMQ example configuration](https://github.com/rabbitmq/rabbitmq-server/blob/v3.11.x/deps/rabbit/docs/rabbitmq.conf.example) to customize [rabbitmq.conf jinja template](./templates/rabbitmq.conf.j2).

For test this role you can use [Molecule](https://ansible.readthedocs.io/projects/molecule/) and [Vagrant](https://www.vagrantup.com/)(Recommended).

Categorize target servers with 3 categories in inventory file:

| Group | Description |
|:-------|:------------|
|**rabbitmq-master**|first node|
|**rabbitmq-slaves**|other nodes|
|**rabbitmq-cluster**|parent of 2 above groups|

For example: **inventory.ini**

```ini
[all]
rabbitmq01
rabbitmq02
rabbitmq03

[rabbitmq-master]
rabbitmq01

[rabbitmq-slaves]
rabbitmq02
rabbitmq03

[rabbitmq-cluster:children]
rabbitmq-master
rabbitmq-slaves

```

Role Variables
--------------

According to [defaults](./defaults/main.yml), you find some variables that you can use on group_vars or host_vars in inventories directory.

Dependencies
------------

Install community-based RabbitMQ Ansible collection:

```bash
ansible-galaxy collection install community.rabbitmq
```

Example Playbook
----------------

```yaml
---
- hosts: all
  become: true
  roles:
    - rabbitmq

```

License
-------

MIT

Author Information
------------------

This role was created in 2023 by [Mohammad Shahmaleki](https://github.com/mshahmalaki), for any suggestions and questions about this ansible role contact with me on [Linkedin](https://www.linkedin.com/in/mohammad-shahmaleki/).
