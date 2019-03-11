---
title: Angular使用Bootstrap时需要注意的坑
date: 2019-03-06 21:10:57
catalogs: Angular
---





# Angular配合BootstrapUI

首先安装bootstrap

```bash
cnpm install bootstrap jquery popper.js --save
```



## Dropdown或是其他动画无效的问题

Bootstrap依赖jQuery，因此首先在angular.json中添加对jquery的引用。

与此同时不要忘记添加bootstrap自身的js库。

```json
            "scripts": [
              "./node_modules/jquery/dist/jquery.min.js",
              "./node_modules/bootstrap/dist/js/bootstrap.min.js"
            ]
```

若要检查jquery是否被引用成功，可在chrome的控制台中进行jquery查询操作确保添加成功。