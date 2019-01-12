---
title: hexo相关
date: 2019-01-11 21:59:18
tags: [hexo]
---

hexo相关设置

### 1、Hexo操作常用命令

```
npm install hexo-deployer-git  #此时当前分支应显示为hexo

```

### 2、换电脑之后的操作

- [hexo系列问题之我们换了电脑怎么办](https://blog.csdn.net/wxl1555/article/details/79293159)

  拉取代码后操作如下命令,该命令会自动安装Hexo相关依赖。

  ```
  npm install hexo-deployer-git  #此时当前分支应显示为hexo
  ```

###3、修改主题next的默认宽度

 	打开编辑`themes\next\source\css\_schemes\Pisces\_layout.styl`，在底部添加如下代码：

```css
// 以下为新增代码！！
header{ width: 75% !important; }
header.post-header {
  width: auto !important;
}
.container .main-inner { width: 75%; }
.content-wrap { width: calc(100% - 260px); }

.header {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.container .main-inner {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.content-wrap {
  +tablet() {
    width: 100% !important;
  }
  +mobile() {
    width: 100% !important;
  }
}
```

