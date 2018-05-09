---
title: yarn更改为淘宝镜像
date: 2018-03-06 20:25:51
categories:
- 技术
- yarn
tags: yarn 
---

// 安装yarn

cnpm install yarn -g 
<!-- more -->
yarn更换下载源

// 查看下载源

yarn config get registry

// 更换为淘宝源

yarn config set registry https://registry.npm.taobao.org

// 初始化项目

yarn init -y

// 安装webpack

yarn add webpack

// 更新到最新的

yarn upgrade webpack

// 安装项目里的依赖

yarn install