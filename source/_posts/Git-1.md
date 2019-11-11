---
title: Git-1
date: 2019-11-11 09:46:09
tags:
---
bare repository
裸版本库（无工作区）
### Git命令
git init
创建版本库
git clone A/B A/B-clone
克隆
git add 文件1 文件2
修改过的文件和新文件加入到下次提交中
git rm
要删除的文件
git commit --message " "
将修改传送到版本库
git pull origin next:master
取回修改
git push 路径 branch
上载修改
git status
检查状态
git diff 文件
显示每个被修改的行
git log
历史 --oneline --graph
