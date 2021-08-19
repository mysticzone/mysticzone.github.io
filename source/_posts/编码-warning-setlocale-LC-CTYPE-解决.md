---
title: '编码''warning: setlocale: LC_CTYPE''解决'
date: 2020-06-01 18:41:56
tags: linux
---
`-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory`
<!--more-->

#### CentOS 提示 `warning: setlocale: LC_CTYPE: cannot change locale (UTF-8)`

**原因**
> 系统上没有对应的UTC-8字符集，而且`LC_CTYPE`也没有设置

```bash
(.py3) root@pan29:~# locale
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
LANG=en_US.UTF-8
LC_CTYPE=UTF-8
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

**修改配置文件**
```bash
cat /etc/environment
LANG=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

```bash
(.py3) root@pan29:~# locale
LANG=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=en_US.UTF-8
```
