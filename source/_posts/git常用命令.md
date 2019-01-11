---
title: git常用命令
date: 2019-01-11 19:12:26
tags:
---

1、拉取远程代码

```
git clone https://github.com/ldjWillow/ldjWillow.github.io.git
git clone -b hexo https://github.com/yourname/ldjWillow.github.io.git   从分支 hexo上拉取代码
```

2、查看分分支

```
git branch     查看本地分支
git branch -r  查看远程分支
git branch -a  查看所有分支(本地和远程)
```

3、创建分支

```kotlin
git branch node0    创建一个名为node0的分支
git push origin node0 创建远程分支（实际上把本地分支node0推送到远程，故node0分支必须在本地先创建）
```

4、切换分支

```
 git checkout node0
```

5、创建并切换分支

```
 git checkout -b node1
```

6、删除分支

```
git branch -d node1 			删除本地分支
git push origin --delete node0  删除远程分支
```

7、拉取分支[git pull](https://www.yiibai.com/git/git_pull.html)

```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
$ git pull origin next:master 
如果远程分支(next)要与当前分支合并，则冒号后面的部分可以省略。上面命令可以简写为： 
$ git pull origin next
```

8、放弃本地修改，强制更新

   git fetch 只是下载远程的库的内容，不做任何的合并 git reset 把HEAD指向刚刚下载的最新的版本

```
git fetch --all
git reset --hard origin/master
```

9、[本地关联远程分支](https://www.cnblogs.com/zhou-chao/p/7678899.html)

```
git branch --set-upstream-to=origin/remote_branch  your_branch
git push --set-upstream origin hexo 
```

10、添加(git add)

[git add all和git add .区别](http://www.softwhy.com/article-8489-1.html)

[git add -A 和 git add . 的区别](https://www.cnblogs.com/skura23/p/5859243.html)

```
git add readme.txt  提交单个文件
git add readme.txt ant.txt 提交多个文件，用空格隔开
git add *.html  提交所有html文件
```







