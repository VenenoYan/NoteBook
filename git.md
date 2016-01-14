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
