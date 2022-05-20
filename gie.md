# git 基本使用

## 安装

[git官网](https://git-scm.com/)

安装完毕后，鼠标右键菜单会多出来两个跟git有关的选项，选择`Git Bash Here`

## 配置
- 配置git用户信息
  >`git config --global user.name "GitHub用户名"`

  >`git config --global user.email "GitHub邮箱"`

- 生成命令`ssh-keygen -t rsa -C "Github邮箱"`

- 生成之后，到`C:\Users\Administrator\.ssh`中找到`id_rsa.pub`文件,`id_rsa`是私钥，不要泄露给别人

- 进入github官网，点击自己头像下的`Settings`进入设置页面

- 点击`SSH and GPG keys`进行配置公钥(`SSH key`)，把`id_rsa.pub`中的内容复制进去即可

- 新建github仓库，名字为自定义

- 会生成一个链接`https://你的github名.github.io/`，在浏览器中输入链接即可访问

## 使用

### 1. 开始新项目
- 创建一个空文件夹作为仓库，尽量是英文

- 执行`git init`让该文件初始化，初始化完成会生成一个.git文件(默认隐藏，`attrib -h .git`可以让其显示)

- 在文件中创建文件，然后执行`git add .`命令

- 执行`git commit -m "第一次提交文件"`，提交文件，添加描述

- 执行`git push`，将代码推向代码库，然后就可以在github上你的仓库中看到你上传的文件

### 2. 接手已有项目
- 在合适位置执行克隆命令，`git clone 仓库地址`，会把远程库的代码克隆到本地文件夹

- 执行`git push -u origin master`，防止后边的命令出错

- 写入需要的代码，然后执行`git add .`

- 执行`git commit -m "对此次修改文件的描述"`，提交文件

- 执行`git push`，将代码推向代码库

## 将本地代码推到github已有仓库的指定分支上

- 将本地文件所在目录变成仓库(初始化)
  > `git init`

- 直接添加所有文件
  > `git add .`

- 给此次操作添加描述
  > `git commit -m "描述"`

- 将本地仓库关联到github仓库上
  > `git remote add origin 仓库地址`

- 创建本地分支，并切换到创建的分支上(此分支名会添加到远程分支上)
  > `git branch 分支名`, `git checkout 分支名`

- 将代码提交到远程分支
  > `git push origin 分支名`

- 会提示输入github的账号密码，输入即可(完成后如果报错，再来一次)

- 如果出现错误信息`fatal: remote origin already exists`，解决办法如下
  > 先执行`git remote rm origin`

  > 在执行`git remote add origin 仓库地址`


## git 常用命令

- `git add .`: 将更改的所有文件添加进入暂存区(会自动识别更改的文件)
  > `git add '文件名'`提交单个文件

- `git status`: 查看当前git所处的状态
  > 放在`git add` 之后可以查看当前都添加了哪些修改的内容

- `git commit -m "本次更改的描述内容"`: 描述内容需要表达本次修改的内容
  > 方便后期查看，禁止不写或乱写

- `git pull`: **在把代码推向代码库之前，必须执行该命令，并看到`Already up to date`才能执行`git push`命令，否则会覆盖别人上传的代码**

- `git push`: 将代码推向代码库
  > **必须在`git pull`执行之后看到`Already up to date`才能执行**

- `git branch`: 查看此项目中都有哪些分支
  > `git branch 分支名`创建分支

  > `git branch -a`查看所有分支(本地 + 远程(前缀为origin))

- `git checkout 分支名`: 切换到某个分支，`git switch 分支名`也可以切换
  > 分支内容修改后建议执行`git push origin 分支名`防止出错

- `git merge 分支名`: 合并分支
  > 将对应分支的代码拿到当前分支下(一般是master)

- `git checkout -- file`: 可以撤销当前文件提交的更改，`git push`之前有效

- `git log`: 查看git的使用记录(日志)
  > `git log --pretty=oneline`可以使日志一行显示(日志id 和 内容描述)

- `git reset --hard HEAD^`: 回退到上一个内容版本
  > `git reset --hard 日志id`可以回退到对应的内容版本

- `git reflog`: 查看每一次的版本控制记录

- `git push origin --delete 分支名`: 删除对应的远程分支
  > 如果发生以下错误
  ```
  error: unable to delete ‘origin/xxxxxxxx-fixbug’: remote ref does not exist
  error: failed to push some refs to ‘git@github.com:xxxxxxxx/xxxxxxxxxx.git`
  ```
  > 解决办法: 切换到该分支上`git checkout 分支名`，再进行删除`git push --delete origin origin/分支名`

### 撤销 commit
`git reset --soft HEAD ^`

`--soft`: 不删除工作空间改动代码，撤销commit，不撤销git add.

`--mixed`: 默认参数，不删除空间改动代码，撤销commit，撤销git add .
  