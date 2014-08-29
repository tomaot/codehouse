关于Codehouse
==============

Codehouse是我编程的代码仓库，开发过程中的代码基本都保存在这个仓库中。

## 学习github的使用

###一、 安装msysgit: Git-1.8.1.2-preview20130201.exe

###二、 配置

####1. C:\Program Files\Git\etc\gitconfig 添加：
【注意！】请将第二行最后的 “your-id” 修改成你在服务器上的实际 id，默认是姓名拼音。

    [alias]

    go = "! bash -c \"git pull && git add .; if [ \\\"$*\\\" == \\\"\\\" ]; then git commit -a; else git commit -am \\\"$*\\\"; fi; git push origin master:your-id;\""

    [core]

    autocrlf = false

    [gui]

    encoding = utf-8

    [i18n]

    commitencoding = GB2312

    [user]

    email = xxx@gmail.com

    name = 某某某

####2. C:\Program Files\Git\etc\inputrc 修改两行为：

    set output-meta on
    set convert-meta off

####3. C:\Program Files\Git\etc\git-completion.bash 末尾增加：

    alias ls='ls --show-control-chars --color=auto'

####4. C:\Program Files\Git\etc\profile 末尾增加：

    export LESSCHARSET=utf-8

###三、密钥

####到开始菜单，找到“Git Bash”，运行之，并执行以下命令：

    $ ssh-keygen -t rsa -C "your_email@example.com"

程序会提示您输入密钥的文件名，直接按回车即可。
然后会要求你输入一个密码，将来在使用密钥的时候需要提供这个密码。可以输入，也可以不输入直接回车（无论输入还是不输入，都会要求你确认一次）。
确认完毕后，程序将生成一对密钥存放在以下文件夹：

C:\Users\Administrator[这里替换成你的用户名]\.ssh
密钥分成两个文件，一个私钥（id_rsa）、一个公钥（id_rsa.pub）。
私钥保存在您的电脑上，公钥交项目负责人添加到服务器上。用户必须拥有与服务器公钥所配对的私钥，才能访问服务器上的代码库。

【注意！】为了项目代码的安全，请妥善保管你的私钥！因为一旦私钥外泄，将可能导致服务器上的代码被泄漏！

    $ clip < C:/Users/Administrator[这里替换成你的用户名]/.ssh/id_rsa.pub

idd_rsa.pub文件的内容复制到剪贴板上，到github网站添加"Add SSH key"

####测试密钥是否有效

    $ ssh -T git@github.com
    
尝试 ssh to github

提示:

    The authenticity of host 'github.com (207.97.227.239)' can't be established.
    RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    Are you sure you want to continue connecting (yes/no)?

 输入yes，

    Hi username! You've successfully authenticated, but GitHub does not provide shell access.
成功！

###四、使用

####add

添加新文件到 Git 代码仓库的索引中

    $ git add filename

####mv

移动或重命名文件

    $ git mv old-filename new-filename

####status

查看目前工作目录的代码状态，自上次提交以来的添加、修改和删除等

    $ git status

####diff

查看自上次提交以来，本地代码改动的具体情况

    $ git diff

####commit

提交修改的代码（只是提交到本地的代码库，不会推送到服务器）

    $ git commit -am '修改说明'

####push

将自上次 push 以来的，本地历次 commit，推送到服务器
结合我们的实际，应该这样写：

    $ git push origin master:your-id

其中，master 是本地的分支名；your-id 填你在服务器上的 id，服务器的版本库里会有以你的 id 为名称的分支。

####pull

将别人推送到服务器的代码，拉到你的机器里

    $ git pull

####log

查看修改记录，含作者、时间、修改说明等

    $ git log

####show

显示具体的代码改动情况
显示最后一次 commit 修改的内容：

    $ git show

显示指定 commit 修改的内容：

####branch

分支管理

列出所有分支（当前所在分支前会有“*”号）：

    $ git branch

新建分支：

    $ git branch 新分支名

删除分支：

    $ git branch -d 欲删除的分支名
    
【注意！】不要把 ‘-d’ 写成了 ‘-D’，危险！

-d：要求：被删除分支的所有修改，已经合并到当前分支；

-D：直接删除，未合并的代码，将被丢弃！

####checkout

恢复某个已修改的文件（撤销未提交的修改）：

    $ git checkout file-name

切换到另外的分支，进行开发：

    $ git checkout branch-name

【注意！】该命令可能伴随大量的文件增删/修改。Windows 下，改动已被占用的文件可能会被拒绝，导致版本库出现严重问题。如果确实要这样做，安全起见，最好先注销一次。

####merge

合并指定分支到当前分支：

    $ git merge branch-name

####revert

还原已提交的修改（已经提交过的修改，可以反悔～）
还原最近一次提交的修改：

    $ git revert HEAD

还原指定版本的修改：

    $ git revert commit-id

####stash

先将未提交的修改暂存起来，接着清除所有改动，使之与没修改时一样。
若你正在开发功能 A，又需立即去开发功能 B。A 的代码正改到一半，未认真整理，你不想立即提交。此时……请呼叫 stash ～。
它会使你所有未提交的修改瞬间不见了：

    $ git stash

它会使刚刚不见了的修改，瞬间又回来了：

    $ git stash pop

####附：git push 失败的解决办法

假设执行操作：

1. 修改代码
2. git commit
3. git push
此时 push 失败（错误提示：! [rejected] master -> master (non-fast-forward) ）

解决办法：

    $ git pull

若成功，则：

    $ git push origin master:your-id
