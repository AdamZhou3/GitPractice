# Git Practice

## ssh config

ssh 用于主机之间的配对，将公钥远程主机使用后会在本地保存在known host文件中

```bash
# second user(second@mail.com)
Host AdamZhou3.github.com
HostName github.com
User git 
IdentityFile ~/.ssh/id_rsa_ucfnhou

# Default github user
Host AdamZh0u.github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_zhouzz400
```

```
eval $(ssh-agent)
## 配置账号ssh
ssh-add ~/.ssh/id_rsa_ucfnhou
ssh-add ~/.ssh/id_rsa_zhouzz400

ssh -T git@AdamZh0u.github.com
ssh -T git@AdamZhou3.github.com
```

[多个github账号ssh配置](https://www.jianshu.com/p/e50aeb57ea57)  
[ssh配置](https://zhuanlan.zhihu.com/p/126117538)  

## git

```bash
git config --global user.email "ucfnhou@ucl.ac.uk"
git config --global user.name "AdamZhou3"

ssh-keygen -t rsa -C "ucfnhou@ucl.ac.uk" ## 设置新密钥
ssh -T git@github.com ## 返回还是AdamZh0u?

git init 
git remote add origin git@github.com:AdamZhou3/i2p-py.git
git checkout -- . ## 从暂存区取回所有
git rm -r --cached . ## 清除所有缓存
```

### init git

```bash 
mkdir learngit
cd learngit
pwd

git init 

touch readme.md
git add readme.md
git commit -m "add a markdown file"
```

### change file and diff
```bash
git status
git diff readme.md

git add readme.md
git commit -m "change file and diff"
git status
```

### git log and reset

- 显示版本
- 回退版本

```bash
git log # 显示版本
git log --pretty=oneline

git reset --hard HEAD^  ##回退一个版本
git log 

git reset --hard 6983  # 根据hash前几位指定版本
```

### stage, add and commit 

```bash
touch license

## change license and readem.md

git status ## 显示工作区 stage 变化
git add readme.md
git status
git add license
git status
git commit

git add readme.md
git add readme.md
git commit ## 多次修改放到暂存区
```

### checkout -- .

回退未add的修改 工作区的修改撤销

```bash
## change readme.md
123

git checkout -- readme.md
```
暂存区的修改撤销  
修改add之后未commit 撤销到上次commit

```bash
123
git add readme.md
git reset HEAD readme.md 
```

两次add 后怎么推到第一次add的？

删除与误删撤销
```bash
rm license 
git status

## 确实要删除
git rm license 
git satus
git commit -m "rm license" ## rm file in folder and in git

## 误删撤销
rm license 
git checkout -- license ## recover
```

### remote repo

```bash
git remote add origin git@github.com:AdamZh0u/GetGit.git ## origin

git push -u origin master ## --upstream 远程origin 
```

### branch create and quick merge 

```bash
## create branch and switch to
git checkout -b dev 

# or 
git switch -c dev
# or 
git branch dev  ## == git branch -c dev
git checkout dev

touch license
## do changes in license 
git add license 
git commit -m "add license to dev"

## 
git checkout master
git merge # quick merge mode

git branch -d dev
```

### git conflict
```bash
git switch -c dev
## change
git add / git commit -m "switch -c dev"/ git push origin dev

git switch master
## change
git add / git commit -m "change in master branch" / git push

git merge dev ## conflicts
## 手动修改
git add .
git commit -m "fix conflict" / git push 

git log --graph --pretty=oneline --abbrev-commit

git branch -d dev
```

### fork workflow

1. fork之后再新分支上开发
2. 先更新fork的分支
3. 从更新的master创建分支用于合并
4. 合并开发分支
5. 重命名合并分支
6. push合并分支，保持master分支与原分支相同
7.pull request

```bash
fork repo1
git clone frepo1
git remote -v # show frepo1
git remote add upstream repo1
git remote -v # show frepo1 repo1

git checkout -b branch master ## branch是用于开发的分支
## changing on branch

git checkout master
git pull upstream master
## pull new changes to local master

git checkout -b branch_merge master ## 从更新后的master分出一个用于合并
git merge branch ## 将本地开发合并到branch_merge
git branch -m branch_merge branch## rename ## 将branch_merge 重命名branch
git push origin branch ## 推送到远程仓库

在github pull request发送请求将branch 合并到原仓库
```

[fork workflow](https://blog.csdn.net/yzpbright/article/details/82180079)

[](https://github.com/dtbootcamp/getting-started-with-git-and-github)


## gitignore config

```
## 添加gitignore
.vagrant/
Vagrantfile
#.gitignore
```
[gitignore 配置](https://www.cnblogs.com/kevingrace/p/5690241.html)  


