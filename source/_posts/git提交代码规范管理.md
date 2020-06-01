---
title: git提交代码规范管理
date: 2020-06-01 09:11:32
categories: 
  - 技术
  - Git
tags: Github
---

### GIT分支管理
- git远程分支主要包括：master develop fixbug

master：整个项目主分支，有且仅有一个，用于管理投产的分支。

develop：develop作为开发分支，命名dev-* 例如: dev-2020-01-10

fixbug：当发生故障或者bug时需要修复，这个时候需要新建一个fixbug分支，命名为fixbug-* 例如：fixbug-2020-01-10
<!--more-->

- git远程分支创建与合并

1.日常开发分支为dev,开发人员只需要在此分支进行开发和代码提交

2.master分支作为投产分支，每次投产定版不能做修改后把本次投产的
dev分支合并到master，并以master分支代码作为投产包

3.fixbug分支修复bug后，合并到master主分支

4.建立新的分支时必须从master主分支去新建

### GIT代码提交规范

1.查看当前代码分支,确保分支无误
```
git branch -a
```

2.查看当前代码修改状态
```
git status
```

3.将当前修改暂存起来
```
git stash
```

4.拉取远程分支代码到本地
```
git pull
```

5.将暂存区代码推出来,有冲突解决冲突
```
git stash pop
```

6.将代码加入缓存区
```
git add .
```

7.将代码提交到个人仓库
```
git commit -m "fix: :bug: 修复了#bug"
```

```
commit-msg 公式：<type>(<scope>): <subject>
  example
  git commit -m "feat(index): 测试提交"
  注意冒号后要有空格
#type：
  feat：    新功能（feature）
  fix：     修补bug 
  docs：    文档（documentation）
  style：   格式（不影响代码运行的变动）
  refactor：重构（即不是新增功能，也不是修改bug的代码变动）
  test：    增加测试

#scope：
   选填，即本次变更的影响范围，可选为（全局、模块名、公共方法/文件名）

#subkect：
   对本次提交的具体描述信息
```

8.提交代码到远程分支
```
git push
```


#### 提交的类型
![](/css/images/git.png)
 
