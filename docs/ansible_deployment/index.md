---
layout: docs
title: Ansible Deployment
group: "navigation"
order: "123"
---

Pundun nodes can be deployed and managed using ansible.
Ansible roles for pundun are developed and tested on ansible **version 2.2.0.0**
To get ansible, follow instructions from [ansible docs](http://docs.ansible.com/ansible/intro_installation.html)
To fetch ansible roles:

```sh
$ git clone https://github.com/pundunlabs/pundun-ansible.git
```

Usage:
Before executing playbooks:

```sh
cd pundun-ansible
export ANSIBLE_HOST_KEY_CHECKING=False
```

Execute deploy role on all defined hosts:

```sh
ansible-playbook -i production site.yml -K
```

Alternatively, depending on hosts defined in production file, execute for a group of hosts.

```sh
ansible-playbook -i production bare_metal.yml -K
```

If hosts are docker containers that are running on local host, you may use docker_play.sh. This script will discover docker hosts and configure production file before executing playbooks.

```sh
./docker_play.sh
```
[top {% include arrow_up %}](#)
