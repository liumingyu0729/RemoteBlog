---
title: Git
date: 2019-11-11 09:46:09
tags: Git
---
bare repository
裸版本库（无工作区）
origin
远程
ssh-keygen -t rsa -C XXX@XXX.com
cat ~/.ssh/id_rsa.pub
### Git命令
git init
创建版本库
git clone A/B A/B-clone
克隆
git remote add origin git@github.com:XXX/XXX.git
指定远程
git add 文件
加入到下次提交中
git rm
要删除的文件
git commit --message " "
将修改传送到版本库
git pull origin next:master
取回修改
git push 路径 branch
上载修改 -u指定一个默认主机
git status
检查状态
git diff 文件
显示每个被修改的行
git log
历史 --oneline --graph
### bash
i 插入模式
Esc
:wq 修改并退出

master 主分支
dev 开发分支
beta 测试版
