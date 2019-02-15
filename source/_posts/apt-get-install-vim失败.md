---
title: apt-get install vim失败
date: 2019-02-13 18:09:54
tags: Linux
---

```bash
$ sudo apt-get install vim
```

失败，提示vim-common版本问题。

解决方案：卸载vim-common并重新安装。

```bash
$ sudo apt-get uninstall vim-common
$ sudo apt-get update
$ sudo apt-get install vim
```

成功。