---
layout: post
title: GitHack
categories: [安全工具]
description: GitHack
keywords: 安全工具 
---

# 简介

https://github.com/BugScanTeam/GitHack.git

> 使用 BugScanTeam 版本效果最好，其他版本不一定成功

https://blog.csdn.net/rfrder/article/details/108391077

## git 信息泄露分类

- git stach
- git log
- git 历史文件

## git 信息查找

git reset --hard HEAD^

git diff HEAD^


## git stach


使用dirsearch扫描发现git泄露，然后githack，进入dist中网站文件夹，右键打开 gitbash，输入git stash list 发现有stash，然后输入 git stash pop ，可以发现在文件夹里出现一个txt文件，打开之后就出现了flag

https://blog.csdn.net/mrwangtw/article/details/120083422

> git stash是git一个很有用的命令，它的作用是把当前未提交的修改暂存起来，让仓库还原到最后一次提交的状态。常用于更新、同步代码或者保存多个修改版本等情况下。

