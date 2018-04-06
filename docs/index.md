---
layout: docs
title: Documentation
group: "navigation"
order: "100"
---
* TOC
{:toc}

### Getting Started


One may install pundun from pre-built packages or from source code.
To install a pre-built package, download desired version form [downloads](/downloads/) page or use pundun [repo](https://packagecloud.io/erdemaksu/pundun) as a software source on target system.

on ubuntu 16.04:

```sh
sudo cp pundun_{{ site.data.global.version }}-1_amd64.deb /var/cache/apt/archives/
sudo dpkg -i /var/cache/apt/archives/pundun_{{ site.data.global.version }}-1_amd64.deb
```

on centos 6.7:

```sh
sudo rpm -Uvh pundun-{{ site.data.global.version }}-1.el6.x86_64.rpm
```

[top {% include arrow_up %}](#) [more on installation {% include arrow_right %}](/docs/installation)

### System Architecture


Pundun Data Management Framework is deigned to be a distributed system, although it could be used as a single node system. Deployment of a multi node system requires configuration of pundun instances and operational tasks which are described in this docs. On this page you will the find minimum to get hands on pundun.

[top {% include arrow_up %}](#) [more on system architecture {% include arrow_right %}](/docs/system_architecture)

### Configuration


Edit '/etc/pundun.yaml';
Modify 'pbp_server_options' parameter.

SSL certificate and key files should be defined here.
To generate self signed certificate files, one may use below commands.

```sh
cd /usr/lib/pundun/lib/pundun-{{ site.data.global.version }}/priv/
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 1095 -nodes
```

#### Configuring SSH Daemon


Edit `/etc/pundun.yaml`.
Modify `pundun_cli_options` parameter.
Under specified `user_dir`, place public and private keys for ssh client.

```sh
cd /usr/lib/pundun/lib/pundun-{{ site.data.global.version }}/priv/ssh
ssh-keygen -t rsa -f <user_dir>/id_rsa
```

Under specified `system_dir`, place public and private keys for ssh host.

```sh
ssh-keygen -t rsa -f <system_dir>/ssh_host_rsa_key
```

Store any public key in `authorized_keys` file at the configured `system_dir`.

#### Starting the pundun node

```sh
service pundun start
# or
pundun start
```

Read local logs from `/usr/lib/pundun/log/local.pundun.log` file.

```sh
service pundun start
# or
pundun start
```

#### Connecting to Command Line Interface


To connect local pundun node`s CLI that is created as above.

```sh
ssh localhost -p 8989
```
Or ssh to remote node that listens on a configured ip and port.
[top {% include arrow_up %}](#)
