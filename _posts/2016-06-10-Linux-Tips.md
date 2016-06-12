---
layout: page
title: Linux Tips
---
# one line command to download and extract files

```sh
$cd /tmp;curl https://www.kernel.org/pub/linux/utils/util-linux/v2.24/util-linux-2.24.tar.gz	| tar -zxf-;cd	util-linux-2.24;
```
# search files contains keyword
```sh
grep -ri 'architect' . | awk -F ':' '{print $1}'
```

# Show Linux kernel and name
`lsb` means Linux Standard Base , `-a` means print all information
```sh
lsb_release -a -u
phray@phray-VirtualBox ~ $ lsb_release -a -u
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 14.04 LTS
Release:	14.04
Codename:	trusty
```
Following is the command found in docker.sh
```sh
lsb_dist=$(lsb_release -a -u 2>&1 | tr '[:upper:]' '[:lower:]' | grep -E 'id' | cut -d ':' -f 2 | tr -d '[[:space:]]')
```

show the 2nd column
```sh
lsb_release --Codename | cut -f2
```
