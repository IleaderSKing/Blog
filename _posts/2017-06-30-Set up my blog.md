---
layout: post
title: "Github pages 搭建个人博客"
excerpt: "教程"
categories:
  - 教程
tags:
  - Git
---
#### 前言：
   - **两个目的：**
     一是自己写点文章、笔记之类的，加深理解。
     二是将自己的项目也放上去，应该可以说方便项目展示和后期管理。（因为刚好我选的模板有个项目模块，可能后期会使用到，于是头脑发热想到这个）

    Ps: 最主要的还是写博文不积极，一直在学习，更新的非常慢。项目这一块后期再挂上去，现在还没有自己的项目。

#### 正文：
  -  前提：

       1.  注册 [Github](https://www.github.com/)  账号
       2. [Git](https://www.git-scm.com/) 基础并且安装好Git
       3. 寻求一个好模板 (我用的模板是基于jeklly构建的)，这里可以找到 [jekyllthemes](jekyllthemes.org)

Ps: 用模板主要还是图省事，自己写很麻烦，耗时间。我选了 [TaylanTatli](https://github.com/TaylanTatli)的模板

- 步骤：
   1. 配置全局user name和email

   ```
     $：git config --global user.name "输入你的用户名"

     $：git config --global user.email "输入你的邮箱"
  ```
   2.  生成ssh key
  ```
  $：ssh-keygen -t rsa -C "输入你的邮箱"
  ```
   3. 在你的Gihub上添加 公钥 ssh key 
   
   4. 初始化git 并增加一个分支（github 规定gh-pages 是呈现页面内容）
```
  $: git init 
  $: git checkout -b gh-pages
```
  
   5. 克隆仓库到本地环境
   ```
   $: git clone https://github.com/TaylanTatli/Halve
   ```

   6. 修改 index.md 文件  （主页）

   7. 修改_data目录下的_config.yml 文件 （相关的配置文件 这里修改标题，图片，联系方式等）

   8. 修改projects.yaml 文件 （这里是放项目链接）

   9. 修改_layouts目录下的文件 （存放的各个页面）

   10. 修改或者添加_posts目录文件 （主要存放markdown文件）

   11. 推送到远程仓库
```
$: git push 
```
Ps: 做完这10个步骤你基本拥有一个自己的博客，期间你要不断推送到远程仓库（至少我是这样子的）。

本人博客地址： https://eval0day7.github.io/Blog/
  

  

