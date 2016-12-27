---
layout: docs
title: Installation
group: "navigation"
order: "115"
---

#### from source:

```sh
git clone https://github.com/pundunlabs/pundun.git
git checkout -b v1.0.3 v1.0.3
make package RELEASE=1
#find your package under ./package/pacages/
#on ubuntu:
mv package/packages/pundun*.deb /var/cache/apt/archives/
ls /var/cache/apt/archives/pundun*.deb | xargs dpkg -i
```

#### from source for developers:

```sh
git clone https://github.com/pundunlabs/pundun.git
rebar3 release
```

#### to manually deploy after build from source:

```sh
git clone https://github.com/pundunlabs/pundun.git
rebar3 as prod tar
# or with erts included
#rebar3 as target tar
```

#### on ubuntu 16.04 using pre-built package:

```sh
sudo cp pundun_1.0.3-1_amd64.deb /var/cache/apt/archives/
sudo dpkg -i /var/cache/apt/archives/pundun_1.0.3-1_amd64.deb
```

#### alternatively using cloud repo;

```sh
curl -s https://packagecloud.io/install/repositories/erdemaksu/pundun/script.deb.sh | sudo bash
sudo apt-get install pundun=1.0.3-1
```

#### on centos 6.7 using pre-built repo:

```sh
sudo rpm -Uvh pundun-1.0.3-1.el6.x86_64.rpm
```

#### alternatively using cloud repo:;

```sh
curl -s https://packagecloud.io/install/repositories/erdemaksu/pundun/script.rpm.sh | sudo bash
sudo yum install pundun-1.0.3-1.el6.x86_64
```

[top {% include arrow_up %}](#)
