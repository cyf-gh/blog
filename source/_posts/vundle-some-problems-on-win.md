---
title: Windows下使用Vundle的若干问题
date: 2019-02-14 17:50:04
categories: Vim
---

关于再Windows下使用Vundle的官方文档详见：[这里](https://github.com/VundleVim/Vundle.vim/wiki/Vundle-for-Windows)

## 错误

常见错误：执行PluginInstall之后所有插件全部安装失败，显示Procession Failed。原因是因为安装Git的时候没有勾选CMD辅助。如果你遇到了类似的情况请打开CMD然后确认curl的版本。

```bash
curl --version
```

如果显示不存在curl，请重新安装Git，并勾选CMD选项。

## 与Linux对应的目录

关于Windows下的Vim各目录。

```bash
vim --version
```

往下翻页就能看见了。

Linux下的.vimrc在Win下为_vimrc，存放位置为

```
C:\Program Files (x86)\Vim
```

Vundle放置于

```
C:\Users\??\.vim\bundle
```

详见 [我的Vundle安装脚本](https://github.com/cyf-gh/Shell/blob/master/vim/install-vundle)