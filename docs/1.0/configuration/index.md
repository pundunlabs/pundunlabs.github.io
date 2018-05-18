---
layout: docs
title: Configuration
group: "navigation"
order: "120"
---
* TOC
{:toc}

### Requirements on System Configuration

It is reccomended to increase the limits for maximum number of open files.
On linux systems one may edit '/etc/security/limits.conf' file to increase 'nofile' to enforce soft and hard limits.

### Configuration of Pundun Nodes

All configuration files are linked from '/etc/pundun/' directory on taget systems. Pundun configuration files are in yaml format and one for each application that pundun includes.

Default values will be set after deployment, but one may like to change these values.

Some important configurations parameters would be:

- pundun.yaml:
    - ppb_server_options: Here. one can edit ip, port and other server settings that listens for pundun protocol buffers defined protocol server.
    - pundun_cli_options: Here, one can edit ip, port and other server settings that listens for pundun command line interface server.
- gb_log.yaml:
    - Customize parameters for global logging settings. One may set a remote host to keep logs on a seperate machine.
- gb_dyno:
    - Customize parameters that are used in distribution management of pundun nodes.
- enterdb.yaml:
    - num_of_local_shards: Default number of shards to be created per database table unless explicitly given at table creation time.
    - db_path: Path to keep the database files.

### Initial configuration of Pundun Nodes
Pundun will load and activate all configurations at the very first start up of the node.
If for some reason a bad configuration, like tcp socket errors based on address in use, causes pundun node to fial start, initial configuration can be removed manually by removing database files.

**Caution**: Use this only if pundun is not being used for any database operation.
This is only to fix initial configuration at very first startup of the node.

```sh
rm /usr/lib/pundun/data/db/*
```

### Reconfiguration of Pundun Nodes

Above mentioned configuration parameters may be edited on live systems and can be loaded and activaed using Pundun CLI.

### Configuration of SSL

SSL related configuratioon parameters are defined in '/etc/pundun/pundun.yaml' file. Specified files that are defined in configuration for 'certfile' and 'keyfile' should be placed under '/usr/lib/pundun/lib/pundun-{{ site.data.global.version }}/priv' directory.

An example command to create key and certificate files named 'key.pem' and 'cert.pem' respectively:

```sh
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 1095 -nodes
```

### Configuration of SSH for CLI access

Configuration parameters are defined in '/etc/pundun/pundun.yaml' for ssh accessof CLI.
One would need to place public and private keys for user and host under the defined 'user_dir' and 'system_dir' repsectively.

```sh
# cd to defined user_dir 
ssh-keygen -t rsa -f id_rsa
# cd to defined system_dir
ssh-keygen -t rsa -f ssh_host_rsa_key
```
