1. git add 先到版本库 再到暂存区??

git 高层命令

git init 初始化仓库

git status 查看文件状态

git add ./ 将修改添加到暂存区

git comit -m 注释 

git diff  查看哪些修改还没有暂存

git diff --staged / git diff --cache 查看哪些修改已经被暂存了还没被提交

### 查看已暂存和未暂存的更新

​	实际上，git status的显示比较简单，仅仅是列出了修改过的文件，如果我们要查看具体修改了什么地方。可以用 git diff 命令。这个命令可以解决两个问题。

​	当前做的哪些更新还没有被暂存，有哪些更新已经暂存起来准备下次提交。

1. 当前做的哪些更新还没有暂存

    git diff （不加参数，直接git diff）

2. 有哪些更新已经暂存起来准备好了下次提交？

    git diff --cached / git diff --staged



### 提交更新

git commit

git commit -m ''

git commit -a -m ''



文件改名  

git mv file.from file.to

git status

其实，运行 git mv 相当于运行了三条命令

mv readme.txt readme

git rm readme.txt

git add readme.txt

git log --pretty=oneline

git log --oneline

### ？

1. github main master
2. clone https, ssh
3. 项目用户 需要在github注册过 才能正常显示

远程仓库配置别名&&用户信息

gir remote add <shortname> <url>

添加一个新的远程仓库

git remote -v

显示远程仓库使用的Git别名与其对应的URL

git remote rename pb paul

重命名

git remote rm [remote-name]

如果因为一些原因想要移除一个远程仓库，你已经从服务器上搬走了或不再像使用某一个特定的镜像了，又或者某一个贡献者不再贡献了。

### 推送本地项目到远程仓库

git remote 别名 仓库地址

初始化一个本地库 

git init

修改用户名和邮箱

git add 

git commit

然后推送本地仓库到远程仓库（清理windows 凭据）：

git push [remote-name] [branch-name] (用户名 密码 附带生成一个远程跟踪分支)

将本地的master分支 推送到origin（别名）服务器。

### 克隆远程仓库到本地

git clone 仓库地址（在本地生成.git文件 默认为远程仓库配了别名 origin）

​								只有在克隆的时候，本地分支 master 和 远程跟踪分支 别名/master 是有同步关系的



邀请别人

成员做出修改

git add

git commit

git push 别名 分支 （输入用户名 密码；推完之后会附带生成远程跟踪分支）。

项目经理修改

git fetch 别名 （将修改同步到远程跟踪分支上。）

git merge 远程跟踪分支。

 远程仓库的名字 'origin' 与分支名字 'master'一样，在 Git 中并没有任何特别的含义一样。同时，'master' 是当你运行 git init 时默认的起始分支名字。'origin' 是当你运行git clone 时的默认远程仓库名字。如果你运行 git clone -o booyah，那么默认你的远程仓库别名为booyah。



### 更新成员提交的内容

git fetch [remote-name]

这个命令会访问远程仓库，从中拉取所有你还没有的数据。（如果发生冲突了怎么办）

执行完成后，你将会拥有那个远程仓库所有分支的引用，可以随时合并或查看。

必须注意 git fetch 命令会将数据拉取到你的本地仓库。他并不会自动合并或者修改你当前的工作。当你准备好时，你必须手动将其合并入你的工作。

### 远程分支

 

### 远程跟踪分支

远程跟踪分支是远程分支状态的引用。它们是你不能移动的本地分支。当你做任何网络通信操作时，他们会自动移动。

他们以 （remote）/ (branch) 形式命名。例如：如果你想要看你最后一次与远程库 origin 通信时master 分支的状态，可以查看 origin/master 分支

当克隆一个仓库时，它通常会自动的创建一个跟踪 origin/master 的 master分支

假设你的网络里有一个 git.ourcompany.com 的git 服务器。如果你从这里克隆，Git的clone命令会为你自动将其命名为 origin，拉取他的所有数据，创建一个指向它的master指针，并且在本地将其命名为 origin/master。Git也会给你一个与 origin/master 分支在指向同一个地方的本地的master分支 。

### 本地分支

设置已有的本地分支跟踪一个刚刚拉取下来的远程分支，或者想要修改正在跟踪的跟踪分支，可以在任意时间内使用 -u 选项运行 git branch来显示设置

git branch -u origin/serverfix(--set-upstream-to)

git branch -u origin/devFornws（新建的本地分支跟踪远程分支）

正常的数据推送 和 拉取步骤

1. 确保本地分支已经跟踪了远程跟踪分支
2. 拉取数据，git pull
3. 上传数据，git push

一个本地分支怎么去跟踪一个远程跟踪分支

1. 当克隆的时候 会自动生成一个master 本地分支 （已经跟踪了对应的远程跟踪分支）

2. 在新建其它分支时，可以指定想要跟踪的远程跟踪分支。

    git checkout -b 本地分支名 远程跟踪分支名

    git checkout --track 远程跟踪分支名

3. 将一个已经存在的分支改成远程跟踪分支

    git branch -u ‘远程跟踪分支’





### 跟踪分支

只有主分支 并且 克隆时 才会自动创建跟踪分支。

跟踪分支是与远程分支有直接关系的本地分支。如果在一个跟踪分支上输入 git pull，Git能自动识别去哪个服务器上抓取，合并到哪个分支。

也可以设置跟踪其他分支或者不跟踪master分支

git checkout -b [branch] [remote name] [branch]

git checkout --track origin/serverfix

git checkout -b sf origin/serverfix

git branch -u origin/serverfix

查看设置的所有远程分支

git branch -vv





删除邮箱名

git config --global --unset user.mail

查看全局信息

git config --global --list

配置项目信息

git config user.name

git config user.email