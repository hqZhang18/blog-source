---
title: TortoiseGit连接gitLab不用每次输入用户名和密码的方法
date: 2018-02-02 17:15:28
categories:
- 技术
- Github
  tags: Github
---

每次git clone 和push 都要输入用户名和密码。虽然安全，但在本机上每次都输有些麻烦，如何记住用户名和密码呢？
<!--more-->
当你配置好git后，在C盘进行查找，有一个  .gitconfig 的文件，里面会有你先前配好的name 和email，只需在下面加一行
[credential] 
     helper = store 

下次再输入用户名 和密码 时，git就会记住，从而在C:\Documents and Settings\Administrator\ 目录下形成一个  .git-credentials 文件，里面就是保存的你的用户名和密码（注意是明文存储！！！）。

这样以后再连接时，就不用再输入用户名和密码了！