# Git常见命令

## 本地仓库

### Git配置

``````git
git config --global user.name xx //设置用户名
git config --global user.email xxxx.com //设置邮箱
git config --global credential.helper store //存储用户凭证
\git config --global http.proxy http://127.0.0.1:7890 //设置代理
``````

### 初始化仓库

本地创建仓库：`git init`

远程拉取仓库： `git clone  仓库地址`

### 当前仓库状态

查看当前git状态：`git status`

### 文件提交

``````git
git add xxx //.表示添加所有改动文件到缓存
git commit -m "xxx" //-m 添加信息，类似此次添加的comm的标题
git commit -am "xxxx" //add commit 合并提交
``````

### 查看提交记录

查看日志：`git log `

查看暂存区的状态： `git ls-files`

### 回退

> [!NOTE]
>
> 工作区：当前可见文件区域， 暂存区：git缓存区域， 当前不可见部分

回退到某一个版本， 保存工作区和暂存区的内容`   git reset --soft`

回退到某一个版本， 丢弃掉工作去和暂存区的内容`  git reset --hard`

回退到某一个版本， 保存工作区的内容，丢弃暂存区的内容` git reset --mix`

### 恢复操作之前版本的命令

查看所用操作的历史纪录：`git reflog `

恢复操作： `git reset --hard xxxx //xxx 为操作的编号`

### 查看比较

> [!NOTE]
>
> 默认比较工作区和暂存区

### 工作区暂存区本地库比较

暂存区比较：`git diff --cached` `git diff` `git stage` 

本地库比较：`git diff HEAD`

### 相同分支的版本比较

`git diff xxx xxx // xxx版本号`

比较上一个版本： `git diff head^`

### 删除暂存区的文件

`get rm xx` // 删除文件需要 commit，此时工作区和缓存区的文件都被删除

`get rm --cached xxx`//只删除暂存区的文件

### 忽略文件

> 需要删除的文件：
>
> 1. 系统或者软件自带的文件，ide自带的文件
> 2. 编译产生的中间文件和结果文件
> 3. 运行时生产日志文件，缓存文件，临时文件
> 4. 涉及身份，口令，密码，密钥等敏感信息文件

将xxx文件添加到ignore里面`echo xxx > .gitignore` 

此时，`git add . git commit -m "xxx"`会默认不会填加xxx到缓存区

举例.gitignore

``````
access.log // 单文件被会略
*.log // 通配符，一类文件被忽略
temp/   // temp下文件被忽略
/TODO //忽略当前目录下TODO文件， 而不忽略subdir/TODo
temp/*.log //忽略temp/ee.log文件， 但是不忽略当前目录下其他子目录下的文件
temp/**/*.log //忽略temp目录下的及其子目录下的文件
``````

编辑.gitignore 文件添加指定文件，或者使用正则文件名来忽略某些文件

*注意：已经添加到暂存区的文件不会被忽略*,删除缓存区该文件，会被.gitignore 重新识别添加，新创建的文件夹下面如果有指定文件会被添加，否则不会被识别添加

#### 分支合并

##### 单分支提交合并

`git commit --amend` //自动合并到上一个提交 

`git rebase -i Head^` //rebase 上一个提交

`git rebase -i Head~X` //rebase 上x个提交

##### 多分支合并

`git merge xxx` //合并分支

`git diff` //冲突解决

git rebase xxx //

> [!TIP]
>
> xxx分支在交点之后的提交合并到当前分支交点之后，当前分支之后的提交会合并到xxx分支的最新提交之后

## 远程仓库

### ssh添加公钥

> [!IMPORTANT]
>
> windows下ssh目录为 **C:\Windows\System32\OpenSSH**， 生成密钥匙时指定文件夹，如果已经生成过密钥，直接回车会导致覆盖前一个密钥，导致前一个密钥的失效，再次生成时需要指定新的文件夹

生成本地公钥 `ssh-keygen -t rsa -b 4096`

`git push` 

`git pull`

本地仓库关联远程仓库

``````
git remote add origin https://github.com/EricSc0ttish/Learning.git
git branch -M main
git push -u origin main
``````







