---
layout: docs
title: Documentation
group: "navigation"
order: "100"
---
* TOC
{:toc}

## Getting Started
This section covers a brief introduction to Pundun and instructions to get you started using it.

### Installing Pundun

#### Prerequisites
- Erlang/OTP version >= 20. Documentation for installing and building Erlang/OTP can be found [here](http://erlang.org/doc/installation_guide/INSTALL.html){:target="_blank"}.
- curl, command line tool for transferring data with URL syntax.


#### Build from source

Pundun can be built using git and rebar3 as follows.

~~~sh
git clone https://github.com/pundunlabs/pundun.git
cd pundun
git checkout -b v{{ site.data.global.version }} v{{ site.data.global.version }}
./rebar3 as prod tar
~~~

This will create a tarball file `_build/prod/rel/pundun/pundun-{{ site.data.global.version }}.tar.gz`.

#### Installation

Unpack pundun-{{ site.data.global.version }}.tar.gz file to desired target location. Below example may require superuser privilages.


~~~sh
adduser pundun
mkdir /opt/pundun
tar xzf _build/prod/rel/pundun/pundun-1.0.8.tar.gz -C /opt/pundun
chown -R pundun:pundun /opt/pundun/
~~~

Create public and private keys for ssh client and server.

~~~sh
su - pundun
cd /opt/pundun/lib/pundun-{{ site.data.global.version }}/priv/ssh/
ssh-keygen -t rsa -f id_rsa
ssh-keygen -t rsa -f ssh_host_rsa_key
~~~


#### Start Pundun

As pundun user:

~~~sh
export PATH=/opt/pundun/bin:$PATH
pundun start
~~~

### Configuring Pundun

#### Requirements on System Configuration

It is reccomended to increase the limits for maximum number of open files.
On linux systems one may edit '/etc/security/limits.conf' file to increase 'nofile' to enforce soft and hard limits.

#### Configuring Pundun Binary Protocol Server

Edit '/opt/pundun/etc/pundun.yaml';
Modify 'pbp_server_options' parameter.

SSL certificate and key files should be defined here.
To generate self signed certificate files, one may use below commands.

```sh
cd /opt/pundun/lib/pundun-{{ site.data.global.version }}/priv/
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 1095 -nodes
```

#### Configuring CLI access

Edit `opt/pundun/etc/pundun.yaml`.
Modify `pundun_cli_options` parameter.
Under specified `user_dir`, place public and private keys for ssh client.

```sh
cd /opt/pundun/lib/pundun-{{ site.data.global.version }}/priv/ssh
ssh-keygen -t rsa -f <user_dir>/id_rsa
```

Under specified `system_dir`, place public and private keys for ssh host.

```sh
ssh-keygen -t rsa -f <system_dir>/ssh_host_rsa_key
```
[top {% include arrow_up %}](#) [more on Configuration {% include arrow_right %}](/docs/1.0/configuration)

### Introduction to CLI

Connect to CLI and change default password (admin:admin).
Use Tab for completion of commands and arguments.

```sh
ssh admin@localhost -p8884
SSH server
Enter password for "admin"
password:
X11 forwarding request failed on channel 0
Welcome to Pundun Command Line Interface
pundun> user passwd admin 4dm1nP@ss
ok
pundun> Connection to localhost closed.
```
[top {% include arrow_up %}](#) [more on CLI {% include arrow_right %}](/docs/1.0/cli)

### Client Drivers and API


[top {% include arrow_up %}](#) [more on installation {% include arrow_right %}](/docs/installation)
