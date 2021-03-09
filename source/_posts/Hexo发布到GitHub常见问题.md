---
title: Hexo发布到GitHub常见问题
date: 2020-04-15 12:14:40
tags: Hexo
---


#### `hexo deploy` 上传 `README.md `到 `github`
1. 将`README.md`问文件移动到`source`目录
2. 在`hexo`的`_config.yml`中设置`skip_render: README.md`


#### `hexo deploy` 每次都要自定义域名
1. 将`CNAME`文件移动到`source`目录
2. 将在`Github Page`中自定义的域名写到`CNAME`里
