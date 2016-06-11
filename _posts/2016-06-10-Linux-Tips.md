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
