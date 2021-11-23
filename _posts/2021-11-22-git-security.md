---
layout: post
title: git泄漏漏洞与危害
categories: git
description: .git的安全漏洞
keywords: 安全, git
---


# ".git" 泄漏漏洞与危害
当前开发人员使用Git进行软件版本控制时，对站点自动部署。如果配置不当的情况下，可能会将“.git”文件夹直接部署到线上环境。这样就引起了“.git”泄露漏洞。
攻击者可以利用该漏洞下载git文件夹里的所有内容。如果文件夹内有敏感信息比如站点源码、数据库账户密码等，攻击者可能直接控制服务器。

# .git目录

 - config - 包含一些配置选项
 - description - 仓库的描述信息，主要给gitweb等git托管系统使用
 - HEAD - 指定当前分支,映射到ref引用，能够找到下一次commit的前一次哈希值
 - hooks - 存放可在某些指令前后触发运行的钩子脚本（hook scripts），默认包含一些脚本样例
 - index - 这个文件就是我们前面提到的暂存区（stage），是一个二进制文件
 - info - 存放仓库的信息
 - objects - 存储所有Git的数据对象,对象的SHA1哈希值的前两位是文件夹名称，后38位作为对象文件名
 - refs - 存储各个分支指向的目标提交
 - branches - 还没发现有什么用处


# Git信息泄露原理
1. 通过泄露的.git文件夹下的文件，还原重建工程源代码
2. 解析.git/index文件，找到工程中所有的（文件名，文件sha1）去.git/objects文件夹下下载对应的文件
3. zlib解压文件，按原始的目录结构写入源代码
> (危害：渗透测试人员、攻击者，可以进一步代码审计，挖掘：文件上传，sql注入等安全漏洞）


# GitHack的使用方法

GitHack是一个.git泄露利用测试脚本，通过泄露的文件，还原重建工程源代码

[GitHack工具](https://github.com/WangYihang/GitHacker)

