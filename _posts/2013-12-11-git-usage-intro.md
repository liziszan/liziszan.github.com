---
layout: post
title: 使用GIT简单教程
categories: [tools]
tags: [git]
---

本文主要是讲述如何简单的使用git来进行版本控制以及协同开发

# 开发流程

基于团队的开发，首先大家都是存在有一个统一的版本控制库，如公司中使用的svn repository, 个人或者很多开源项目（如linux, chromium, android等）使用git来进行版本控制，（注：git的作者就是linux的作者）。那如何使用git来进行版本控制和协同开发呢？

## 1. clone库(只需要第一次clone回来即可)

如我们现在的代码库为 `https://github.com/liziszan/php.git`， 那么执行`git clone`,得到如下的结果：

{% highlight bash %}
brianli@sunrise ~/Downloads$ git clone https://github.com/liziszan/php.git
Cloning into 'php'...
remote: Counting objects: 17, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 17 (delta 2), reused 16 (delta 1)
Unpacking objects: 100% (17/17), done.
Checking connectivity... done
brianli@sunrise ~/Downloads$
{% endhighlight %}

## 2. 对代码进行增删改操作

协同开发吧，自己获取到了代码之后就需要写一些代码，下面以增加代码为例说明如何操作：

### 2.1. 增加文件loop.php

如在php/php_study目录下（即index.php文件旁边）增加一个loop.php文件，里面写如下面的代码：

{% highlight php %}
<?php

for ($i = 0; $i < 10; $i++) {
  echo "i = $i\n";
}

?>
{% endhighlight %}

### 2.2. 查看php这个git库下的状态

使用`git status`来查看

{% highlight bash %}
brianli@sunrise /data/lizan/php$ git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	php_study/loop.php
nothing added to commit but untracked files present (use "git add" to track)
{% endhighlight %}

发现存在有一个php_study/loop.php文件没有由git来进行管理

### 2.3. 将文件加到git下进行管理

使用`git add`将没有放到git管理下的文件下进行管理

{% highlight bash %}
brianli@sunrise /data/lizan/php$ git add *
brianli@sunrise /data/lizan/php$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	new file:   php_study/loop.php
#
{% endhighlight %}

### 2.4. 将文件提交到本地git库中

若觉得编写的代码没问题的话，可以将刚刚编写的代码提交到本地的git库中去， 提交命令是`git commit`，

{% highlight bash %}
brianli@sunrise /data/lizan/php$ git commit -a -m "add loop test"
[master 7f9b558] add loop test
 1 file changed, 7 insertions(+)
 create mode 100644 php_study/loop.php
{% endhighlight %}

其中`git commit -a -m `中的-a是自动添加的意思，-m就是说给本次提交起个名字，就是说这次提交的原因和目的是啥

### 2.5. 将git从本地推到github上取

`git commit`只是将增删改的文件提交到本地的git库中，只有自己一个人能够看到，为了其他的人也可以看到，方便给你指导，需要将代码从本地提交到远程的github上

提交命令为`git push`，即将本地的git库推到远程的github上去

{% highlight bash %}
brianli@sunrise /data/lizan/php$ git push
Counting objects: 6, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 370 bytes | 0 bytes/s, done.
Total 4 (delta 1), reused 0 (delta 0)
To https://github.com/liziszan/php.git
   df1949d..7f9b558  master -> master
{% endhighlight %}

这里面有可能要你输入用户名和密码，用户名是liziszan@gmail.com, 密码你懂的

`git push`完之后，就可以在远程的git库[loop.php](https://github.com/liziszan/php/blob/master/php_study/loop.php)上看到对应的代码了

## 更复杂的git操作

上面的只是涉及到最基础、最简单的git操作，如想了解更加复杂的，可以查看我之前写的一篇博客[如何使用git](http://blog.wzgtech.com/2013/09/use-git/)