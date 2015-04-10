---
layout: default
title: Installation
group: "navigation"
order: "105"
---

# Installation of the framework

Code base of the frame work is hosted on **skelter**.
To contribute to development, contact the administrator of skelter.

## Growbeard Resource Management, Build and Release Tool

> IMPORTANT! If erl_leveldb app is going to be built, due to usage of dirty nifs in leveldb wrapper, OTP version 17 is required and OTP should be built with option **--enable-dirty-schedulers**

To install the system:

- Clone the git repository.
 --http://skelter/gits/growbeard.git 
- Get dependencies, build and release using growbeard script as shown below.

### Quick Start

```sh
$ git clone http://skelter/gits/growbeard.git
$ cd growbeard
growbeard$ ./growbeard get_deps
growbeard$ ./growbeard configure
growbeard$ ./growbeard build
growbeard$ ./growbeard rel
```

> Currently there is no command defined for configure phase.
> See example manifest file and reltool.config under examples/

### Repository Structure
This repo includes:

- growbeard: Single script to execute resource management, configuration, building and release handling.
 - Optionally place the script "growbeard" in your path.
- manifest: Declaration file for resources, command and configuration.

Directory structure is as follows:

```sh
$ tree growbeard/
$ growbeard/
$ |-- examples
$ |   |-- manifest
$ |   `-- reltool.config
$ |-- growbeard
$ |-- manifest
$ |-- README.md
$ `-- rel
$     |-- reltool.config
$     `-- runscript
```

- reltool.config: Erlang Reltool configuration file that includes system configuration.
 - Default declares profile as development. Change to embedded or standalone for installation packages.
- runscript: The script to start, stop, attach to released erlang nodes.

### Growbeard usage

```sh
growbeard$ ./growbeard --help 
Usage: growbeard COMMAND [MANIFEST_FILE]
where OPTION :: build | get_deps | rel
      MANIFEST_FILE :: <PATH_TO_FILE> 

```

Manifest file syntax is as follows.

```sh
LINE:
    COMMENT | EMPTY | PHASE_START | OPERATION
COMMENT:
    #*
EMPTY:
    
PHASE_START:
    get_deps: | configure: | build: | rel:
OPERATION:
    GET_DEPS_OP | CONFIGURE_OP | BUILD_OP | REL_OP
GET_DEPS_OP:
    <GIT_URL>
CONFIGURE_OP:
    <SHELL_CMD>
BUILD_OP:
    <APP_NAME>
REL_OP:
    <PATH_TO_RELTOOL_CONFIG> | <CP_CMD> | <MKDIR_CMD>
```

An example manifest file is as follows:

```sh
 get_deps:
 [<GIT URL>]
 configure:
 [<COMMAND>]
 build:
 [<DIR_NAME_UNDER_SRC>]
 rel:
 <rel/reltool.config>
 [<MKDIR CMD> || <CP_CMD>]
```

## Configuring and Starting the System

```sh
growbeard$ cd rel
rel$ pundun/bin/pundun help
Usage: pundun {start|stop|attach|configure}
rel$ pundun/bin/pundun configure
rel$ pundun/bin/pundun start
Starting pundun
rel$ pundun/bin/pundun attach
Attaching to pundun
....
(pundun@<HOSTNAME>)1> [Quit]
rel$ pundun/bin/pundun stop
Stopping pundun
==> ok
```

