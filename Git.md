## 资料

### 书籍

1、Github入门与实践

2、Git高手之路

### 网页

1、Git Reference

[Git - Reference (git-scm.com)](https://git-scm.com/docs)

2、Git 备忘单

[GitHub Git 备忘单 - GitHub Cheatsheets](https://training.github.com/downloads/zh_CN/github-git-cheat-sheet/)

3、gitignore模板

[github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore)

4、Git cheatsheet

[stash :: Git Cheatsheet (ndpsoftware.com)](https://ndpsoftware.com/git-cheatsheet.html#loc=stash;)

5、Git菜鸟教程

[Git 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/git/git-tutorial.html)

6、Git教程

[Git简介 - 廖雪峰的官方网站 (liaoxuefeng.com)](https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000)

### 企业应用

### 问题

1、Git的五个工作区域是哪些？

2、如何对Git进行配置？

3、分支相关操作？

4、如何重做提交？

5、如何关联远程仓库？

6、git pull和git fetch的区别？

7、HEAD的含义？

### 问题答案

1、存档库(Stash)、工作区(Workspace)、暂存区(Index)、本地版本库(Local Repository)、上游版本库(Upstream Repository)

2、git config --global等命令，可以配置姓名、邮箱、颜色显示

3、git branch、git checkout和git merge

4、git reset (--hard) [commit]

5、git remote add origin url

6、git pull = git fetch + git merge

7、HEAD表示当前的工作目录，使用git checkout可以移动HEAD指针到不同分支、标记或提交。

### 其他

git branch

git merge

git stash

git 回退

## 1 Git简介
- 分布式版本控制系统
## 2 创建版本库
- git init：将目录变成Git可以管理的仓库
- git add：把文件添加到版本库
- git commit：把文件提交到版本库
## 3 时光机穿梭
- git status：查看文件状态
- git diff：查看文件哪里修改了，直接使用查看源文件是否被更改，而不是源文件和分支的区别
- git diff HEAD -- readme.txt查看readme.txt文件在工作区和版本库中的区别
### 3.1 版本回退
- git log：查看最近3次提交日志
- commit id：git通过SHA1计算出来的数字，表示版本号
- **HEAD表示当前版本，上一个版本为`HEAD^`，上上一个版本为`HEAD^^`，上100个版本为`HEAD~100`**
- git reset：回退版本，有--hard强制选项，可以使用HEAD或版本号
- git reflog：显示每一次命令
### 3.2 工作区和暂存区
- 工作区：电脑里能看到的目录
- 版本库：工作区中的隐藏目录.git
- 版本库里保存了stage暂存区、master分支以及指向master的指针HEAD
- git add将文件修改添加到暂存区
- git commit将暂存区的所有内容提交到当前分支
### 3.3 管理修改
- git跟踪并管理的是修改，而非文件
### 3.4 撤销修改
- 场景一：修改还没放到暂存区，使用git checkout -- readme.txt（从暂存区或版本库拉取到工作区）
- 场景二：修改已放到暂存区，使用git reset HEAD readme.txt，恢复到场景一
- 场景三：修改已提交到本地仓库，使用git reset --hard HEAD^
- 场景四：修改已提交到远程仓库，。。。，没救了
### 3.5 删除文件
- git rm：删除一个文件
- git checkout实际上是将版本库中的版本替换工作区的版本
## 4 远程仓库
- 使用git时，一般找一台电脑充当服务器的角色
- 可以使用github作为代码托管服务
- 本地git仓库和github仓库之间通过ssh加密
- 设置github仓库步骤：创建SSH Key；在github中添加公钥；
- 创建SSH Key：使用ssh-keygen命令创建公钥和密钥，id_rsa和id_rsa.pub
- 在github 中添加公钥：github需要识别你推送的提交确实是你推送的
### 4.1 添加远程库
- 将本地仓库关联到远程库：git remote add origin git@github.com:username/repository.git
- origin为远程库默认名称
- 推送内容到远程库：git push -u origin master
- 第一次推送使用-u选项，将分支和远程分支关联起来，以后推送可以简化命令
- 查看远程库：git remote -v
- 删除远程库（解除本地和远程的绑定关系）：git remote rm origin
### 4.2 从远程库克隆
- 从零开发，最好先创建远程库，再从远程库克隆
- git clone即可
- ssh协议比https协议快
## 5 分支管理
- 使用分支方便开发新功能，不会干扰到别人的开发
- 分支开发完毕后，一次性提交
### 5.1 创建与合并分支
- master为主分支，指向提交，HEAD指向master
- 创建新分支dev，则dev指向当前提交，同时HAED指向dev，表示当前分支在dev上
- 在dev分支上工作，dev指针会变化，而master指针不变
- 分支合并：将master指向dev的当前提交
- 创建分支：git branch dev
- 切换分支：git checkout dev
- 创建并切换分支：git checkout -b dev
- 查看分支：git branch
- 合并分支：git merge dev （合并dev到当前分支）
- 删除分支：git branch -d dev
- 创建和切换分支的另一种方式：git switch -c dev
- git鼓励使用大量分支
### 5.2 解决冲突
- 两个分支各自都做了修改，就无法执行快速合并，只能试图将各自的修改合并起来
- 合并时可能会发生冲突，必须手动解决冲突后再提交
- git status可查看冲突的文件
- git用`<<<<<<`，`======`和`>>>>>>`标记出不同分支的内容
- git log --graph可查看分支合并情况
- 解决冲突就是把git合并失败的文件手动编辑为我们希望的内容，再提交
### 5.3 分支管理策略
- 使用快速合并方式合并分支，删除分支后会丢失分支信息
- git merge --no-ff强制禁用快速合并模式
- master版本应该非常稳定，只用来发布新版本
- dev版本不稳定，每个人在dev上干活
- 每个人在dev分支再拉一个新的分支干自己的活，干完合并到dev分支
### 5.4 Bug分支
- 每个bug可以通过一个新的临时分支修复，修复后合并分支，然后将临时分支删除
- git stash可以将当前工作现场暂存，等以后恢复现场后继续工作
- git stash list查看暂存的内容
- git stash apply：恢复现场后stash内容并不删除，需要用git stash drop删除
- git stash pop：恢复的同时将stash内容删了
- git cherry-pick：复制特定提交到当前分支
- 切换分支时工作树应该是clean的，不能有未提交或未暂存的修改，所以需要用git stash暂存内容，切换回该分支后恢复现场
### 5.5 Feature分支
- 添加新功能时最好新建一个feature分支
- git branch -D <name>：强制删除一个没有被合并过的分支
### 5.6 多人协作
- 查看远程库：git remote 或 git remote -v
- master分支为主分支，要时刻与远程同步
- dev分支是开发分支，也要与远程同步
- bug分支只用于本地修复bug，一般不必推送到远程
- feature分支是否推到远程，取决于是否合作开发
- 在git中，分支可以本地藏着玩
- git clone时，默认只能看到master分支
- git checkout -b dev origin/dev：创建本地dev分支，并关联到远程dev分支
- 如果自己推送时远程对应分支已被修改，需要git pull将最新提交抓下来，在本地合并后解决冲突，再推送
- git pull --set-upstream-to=origin/dev dev：设置dev和远程origin/dev链接
### 5.7 Rebase
- git rebase：push操作发生冲突时，需要拉到本地合并再提交，使提交有很多分叉，使用git rebase减少提交历史的分叉
- rebase操作：将分叉的提交历史整理成一条直线
## 6 标签管理
- 标签实际上就是一个版本号，方便记住
- 标签和commit id类似
### 6.1 创建标签
- git tag <name>：给当前分支打标签
### 6.2 操作标签
- git push origin <tagname>：推送标签
## 7 使用github
- 将开源库fork到自己账号，然后clone下来（这样才可以修改）
- 修改完后推送到自己的远程仓库中，然后在github上发起pull request