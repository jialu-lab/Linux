# 基本操作

**git** **pull**
git add README.md             只README.md文件加入本地库以备提交
git add .                     所有改动加入本地库以备提交
git commit -m "first commit"  提交到本地
git push                      提交到远程

# 分支操作

**git branch dev  新建dev分支**
**git checkout dev 切换dev分支，会自动关联远程同名分支**
**git checkout -b dev  新建并切换dev分支**
**git checkout -b dev origin/dev 本地与远程关联，并checkout，远程库默认名是origin**
**git branch --set-upstream-to=origin/dev 将本地分支和远程分支关联**
**git branch --unset-upstream dev 取消与远程分支关联**

**git branch -a 查看本地和远程所有分支**
**git branch -r 查看远程分支**
**git branch -d dev 删除dev分支**

**git branch -vv 查看与远程分支关联情况**

**git checkout --track origin/dev 从服务器拉去dev分支，使用--track参数**
**git push origin dev  提交本地分支到服务器上**
**git push origin dev:dev  不在该分支时提交分支数据，需要指定 本地分支:远程分支**

# 使用远程库覆盖

**git fetch —-all  本地库获取所有**
**git reset --hard origin/master  本地库reset为远程库，***注意如果远程分支上文件夹改名的话可能本地的文件夹依然会存在**
**git pull 拉回工作目录**

# 关联远程库

**git remote add origin **[git@github.com](mailto:git@github.com):xxx/xxx.git  关联远程库**
**git push -u origin master 关联主机和分支

**git reset HEAD^ 本地库回滚**

**git remote -v  查看远程库路径**
**git remote add upstream **[git@github.com](mailto:git@github.com):xxx/xxx.git 配置远程库与源库关联**
**git fetch upstream 与源库同步

# 新建分支，提交合并操作

**git branch iss**
**git checkout iss**
**git add file**
**git commit -m 'add file'**
**git push --set-upstream origin iss #在远程库也建分支**

**git checkout master #回到master**
**git merge iss #合并**
**git branch -d iss**
**git push**
**git push origin --delete iss #删除远程分支**
**git push origin  :iss #或者推一个空分支到远程，删除远程分支**

# 修改已经提交的作者信息，rebase最好在本地操作，如果已经push提交远程最好不要rebase

**git log**
**git rebase -i hashcode/head #出现vim编辑，把pick改为edit，:wq退出**
**git commit --amend --author='qingspace **[qingspace@163.com](mailto:qingspace@163.com)'**
**git rebase --continue #结束修改

# 可以看到head

**git log --oneline -n5**

# 强行回滚提交远程库，不留记录

**git reset --hard HEAD^  #HEAD~1 前一个版本**
**git push  --force**

# 删除

**git rm --cached -r .idea**
**git commit -m 'delete .idea'**
**git push origin master**

# 查看remote地址和本地对应关系等信息

**git remote show origin**

# 清理远程已经删除的分支

**git remote prune origin**

# 取消私钥中的密码，Visual Code不支持有密码：

**openssl rsa -in ~/.ssh/id_rsa -out ~/.ssh/id_rsa_new**
**mv ~/.ssh/id_rsa ~/.ssh/id_rsa.backup**
**mv ~/.ssh/id_rsa_new ~/.ssh/id_rsa**
**chomd 600 ~/.ssh/id_rsa**

# 彻底删除版本库某个文件夹或文件

## 删除

**git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch fix-client-py/venv/xx.db' --prune-empty --tag-name-filter cat -- --all**
**git filter-branch --force --index-filter 'git rm -r --cached --ignore-unmatch fix-client-py/venv/' --prune-empty --tag-name-filter cat -- --all**

## 提交远程

**git push -u origin master --force**

## 清理本地库

**rm -rf .git/refs/original/**
**git reflog expire --expire=now --all**
**git gc --prune=now**
**git gc --aggressive --prune=now**

# 计算代码行数

**根据：当前分支+作者+时间段**
**git log --author=zengtai --since=2020-05-11 --until=2020-06-03 --format='%aN' | sort -u | while read name; do echo -en "**name\t"; git log --author="**name" --pretty=tformat: --numstat | grep "**(**.html**|**.java**|**.xml**|**.properties**)**$" | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -; done
根据：当前分支+作者
git log --author="zengtai" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -;
根据：当前分支（整个项目）
git log  --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }';**
