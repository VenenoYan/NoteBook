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
删除：
    git rm file1
    git commit -m ...
删除回复：
    git checkout --file
HEAD永远指向当前工作分支
```