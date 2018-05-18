---
layout: docs
title: Installation
group: "navigation"
order: "115"
---
* TOC
{:toc}

#### on ubuntu 16.04 using pre-built package:

```sh
sudo cp pundun_{{ site.data.global.version }}-1_amd64.deb /var/cache/apt/archives/
sudo dpkg -i /var/cache/apt/archives/pundun_{{ site.data.global.version }}-1_amd64.deb
```

#### on centos 6.7 using pre-built repo:

```sh
sudo rpm -Uvh pundun-{{ site.data.global.version }}-1.el6.x86_64.rpm
```

#### from source:

> If you are building from source, keep in mind to enable dirty schedulers while building Erlang OTP. Erlang OTP version should be >= 19.

```sh
git clone https://github.com/pundunlabs/pundun.git
cd pundun
git checkout -b v{{ site.data.global.version }} v{{ site.data.global.version }}
make package RELEASE=1
#find your package under ./package/packages/
#on ubuntu:
mv package/packages/pundun_{{ site.data.global.version }}-1_amd64.deb /var/cache/apt/archives/
ls /var/cache/apt/archives/pundun_{{ site.data.global.version }}-1_amd64.deb | xargs dpkg -i
```

#### from source for developers:

```sh
git clone https://github.com/pundunlabs/pundun.git
cd pundun
rebar3 release
```

#### to manually deploy after build from source:

```sh
git clone https://github.com/pundunlabs/pundun.git
cd pundun
rebar3 as prod tar
# or with erts included
#rebar3 as target tar
```

[top {% include arrow_up %}](#)
