1. 
安装
1. 
配置
```C
配置文件：
    1)etc/.gitconfig   以下全是system
    2)~/.gitconfig     用global,当前用户。也是默认的
    3)./.git/config    本仓库
$git config [--global] user.name "yourname"
$git config [--global] user.eamil "email"    // global/system/无
$git config [--global] color.ui true   颜色
$git config [--global] alias.st status  重命名命令
$git config [--global] core.editor vim/emacs    设默认编辑器
$git config [--global] merge.tool vimdiff       比较工具
```
1. 
本地使用
```C
        工作区--add-->暂存区--commit-->版本仓库
git init        :初始化一个本地仓库
git add file1 file2 ... :添加文件
git add ./-A/-u  :  添加所有除了删除的/添加所有/添加除新建之外的
git commit -m "instruction" [-a] :  提交的说明。加[-a]只对已提交过的文件有效
git status  : 仓库状态
git diff file1  ： 文件file1的改动
git log [--pretty=oneline]  历史记录
git reflog   查看历史commit-id
git blame file1  查看文件被修改的信息
版本回退：
    1)仍在工作区未add:  git checkout --filename1  返回到最近的已提交状态
    2)已提交commit：   git reset --hard HEAD~[i]  回退（后再执行一次1)）
前进：回退多了
    git reset --hard commit-id
删除文件：
    git rm file1
    git commit -m ...
删除回复：
    git checkout --file
HEAD永远指向当前工作分支
git checkout 把版本库中的文件覆盖工作区文件
分支：
    git checkout -b [Bname] 新建并切换
    git branch [Bname]       新建分支
    git checkout [Bname]     切换分支
    git branch -d/-D [Bname] 删除/强制删除
    git push [remote-name] --delete [Bname] 删除远程分支
    git merge [Bname]        把分支合并到当前分支
    合并时会有冲突：默认Fast-forward模式,自己解决
        git merge --no-ff -m "instruction" [Bname]
分支信息：
    git branch -v       本地分支信息
    git remote -v       远程分支url
    git branch -r       远程分支名
    git branch -m [old] [new] 改分支名字
保存当前工作环境：
    git stash       保存现场
        do something else
    git stash apply [id]
    git stash drop  删除
    git stash pop    恢复现场，相当于上面两个指令
    git stash list      所有
```
1. 
远程库
```C
首先认证：
    ssh-keygen -t rsa -C "youremail"  
    然后把生成的 id_rsa.pub内容放到github内
绑定：
    git remote add [remote-name] git@github:[yourname]/[respo_name].git
使用：
    git pull
    git push [remote-name] [localB-name]
    git fetch
远程到本地：
    git clone [url]
推送：
    git checkout -b [lBname] [remote-name/Bname]  :建立对应远程的分支名，最好名字相同
    git push [remote-name/Bname] [localB-name]  ：  指定分支推送
分支关联：
    1)普通：git remote add ....
    2)指定分支： git branch --set-upstream [local/lBname] [remote-name/Bname]
删除：
    1)删除远程分支：
        git push [remote-name] --delete [Bname]
    2)删除远程仓库绑定：
        git remote rm [remote-name]
修改：
    git remote set-url --push [remote-name] new-url
重命名：
    git remote rename [old] [new]
```