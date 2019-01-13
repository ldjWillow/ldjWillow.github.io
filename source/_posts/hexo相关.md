---
title: hexo相关
date: 2019-01-11 21:59:18
tags: [hexo]
copyright: true
---

hexo相关设置

<!-- more -->

#### Hexo操作常用命令

```
npm install hexo-deployer-git  #此时当前分支应显示为hexo
```

#### 阅读全文

在文章合适的位置添加`<!-- more -->`，Hexo推荐使用。

#### 换电脑之后的操作

- [hexo系列问题之我们换了电脑怎么办](https://blog.csdn.net/wxl1555/article/details/79293159)

  拉取代码后操作如下命令,该命令会自动安装Hexo相关依赖。

  ```
  npm install hexo-deployer-git  #此时当前分支应显示为hexo
  ```

#### 给主题next添加搜索功能

- 安装插件

  ```
  npm install hexo-generator-searchdb --save
  ```

- 修改配置文件

  路径：/blog/themes/next下的_config.yml文件，进行编辑

  ```
  local_search:
      enable: true
  ```

#### 修改主题next的默认宽度

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

#### 常见问题

 ##### hexo的表体无法渲染Markdown语法

​       在##后面加空格,如

  ```
## 二级标题
  ```

#### 参考链接

> * [2018最新版Hexo博客Next主题6.0配置优化](https://blog.csdn.net/qq_32454537/article/details/79482896)
> * [hexo的next主题个性化教程：打造炫酷网站](https://blog.csdn.net/qq_33699981/article/details/72716951)
> * [[Next主题个性化设置](https://www.cnblogs.com/liziczh/p/9318656.html)](http://www.cnblogs.com/liziczh/p/9318656.html)
> * [Hexo设置主题以及Next主题个性设置](https://www.jianshu.com/p/b20fc983005f)