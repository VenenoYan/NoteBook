
### 安装

```C
linux下安装：(window是图形界面)
sudo add-apt-repository ppa:webupd8team/sublime-text-3: 建立信任数据库
sudo apt-get update
sudo apt-get install sublime-text-installer```
    增加Sublime Text的安装目录到系统环境变量path中
    安装Package Contrl(sublime text 3):
        import urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' +
        'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp =
        sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener(
        urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://sublime.wbond.net/' +
        pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating
        download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else
        open(os.path.join( ipp, pf), 'wb' ).write(by)
## 快捷键：
```C
    所有的默认快捷键都在preferendes->key binds default 中，可以设置key binds user 中重新设置
    
ctrl + `            打开控制台
ctrl + shift+p      打开package control
Tab                 向后缩进
Shift + Tab         向前缩进
Ctrl + Enter        在当前行下面新增一行然后跳至该行；
Ctrl + Shift + Enter 在当前行上面增加一行并跳至该行
Ctrl + ←/→          进行逐词移动鼠标
Ctrl + Shift + ←/→  进行逐词选择。
Ctrl + ↑/↓          移动当前显示区域
Ctrl + Shift + ↑/↓  移动当前行
Ctrl + D            选择当前光标所在的词并高亮(使用 Ctrl+K 跳过，使用 Ctrl+U 进行回退，使用Esc退出多重编辑)
Alt + F3            当前词的所有位置
Ctrl + Shift + L    同时编辑(先选择要同时编辑的区域)
Ctrl + J            把当前选中区域合并为一行

Ctrl + F            搜索
Ctrl + H            替换
         Enter跳至关键字当前光标的下一个位置，Shift + Enter跳至上一个位置，Alt + Enter出现的所有位置
         Alt + C切换大小写敏感   Alt + W切换整字匹配
        
Ctrl + P            列出当前打开的文件
    在Ctrl + P匹配到文件后，我们可以进行后续输入以跳转到更精确的位置：
        @ 符号跳转：    输入@symbol 跳转到symbol符号所在的位置
        # 关键字跳转：  输入#keyword 跳转到keyword所在的位置
        : 行号跳转：    输入:12 跳转到文件的第12行。
    
Ctrl + R            列出当前文件中的符号
Ctrl + G            然后输入行号以跳转到指定行
Ctrl + Shift + N    创建一个新sublime窗口
Ctrl + N            创建一个新标签
Ctrl + W            关闭当前标签
Ctrl + Shift + T    恢复刚刚关闭的标签
Ctrl+Shift+W        关闭所有打开文件
Ctrl+X              删除当前行
Ctrl + Shift + [    折叠
Ctrl + Shift + ]    打开折叠
Alt + Shift + 2     进行左右分屏    
Alt + Shift + 8     进行上下分屏
Alt + Shift + 5     进行上下左右分屏（即分为四屏）
Ctrl + 数字键        跳转到指定屏
Ctrl + K / B        显示或隐藏侧栏
Ctrl + M            可以快速的在起始括号和结尾括号间切换
Ctrl + Shift + M    则可以快速选择括号间的内容
```


## 个性化：

preferences->settings-User 中设置
```C
{
	"color_scheme": "Packages/Color Scheme - Default/Solarized (Light).tmTheme", (提前P-C安装)
	"font_size": 15,
	"highlight_line": true,
	
	// 设置tab的大小为2
    "tab_size": 4,
    // 使用空格代替tab
    "translate_tabs_to_spaces": true,
    // 添加行宽标尺
    "rulers": [80, 100],
    // 显示空白字符
    "draw_white_space": "all",
    // 保存时自动去除行末空白
    "trim_trailing_white_space_on_save": true,
    // 保存时自动增加文件末尾换行(项目有这样的要求?)
    "ensure_newline_at_eof_on_save": true,
    
	"ignored_packages":
	[
		"Vintage"
	]
}

```

## 一键运行python ：

在preferences->key binding 中
```C
[
       { "keys": ["ctrl+q"], "command": "repl_open",
                 "caption": "Python",
                 "mnemonic": "p",
                 "args": {
                 "type": "subprocess",
                 "encoding": "utf8",
                 "cmd": ["python", "-i", "-u", "$file"],
                 "cwd": "$file_path",
                 "syntax": "Packages/Python/Python.tmLanguage",
                 "external_id": "python"
                 }
    }
]
```


## 一键运行c++：

在tools->build system->new 新建一个即可,(一般已带)
```C
{
     "cmd": ["g++", "${file}", "-o", "${file_path}/${file_base_name}"],
     "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
     "working_dir": "${file_path}",
     "selector": "source.c, source.c++",
     "encoding": "cp936",
     "shell": true,

     "variants":
     [
          {
               "name": "Run",
               "cmd": [ "start", "${file_path}/${file_base_name}.exe"]
          }
     ]
}```


## 常用插件：
```C
sublimetepl:        html,css,js 模板
GitGutter:          记录改动
brackethighlight：  高亮匹配
converttoutf8:      中文乱码
HTMLBeautify：      格式化HTML。
AutoPEP8：          格式化Python代码。
Alignment：         进行智能对齐。
HTML/JS/CSS prettify  格式化HTML/JS/CSS
PEP8 Autoformat     python pep8自动格式整理
ColorHighlighter    css颜色高亮
Sublime-HTMLPrettify  一个html js 和css代码美化的插件
Autoprefixer        可以给css自动加前缀功能
jQuery              支持jquery的只能语法提示
CSS3                CSS3的自动补全
SublimeLinter       可以验证各种语法错误。
ConvertToUTF8       自动转换乱码
DocBlockr           对代码建立文档。会解析函数，变量，和参数，自动生成文档范式，你的工作就是去填充对应的说明。
AllAutocomplete     自动完成插件(全部打开的文件中，自动完成)
ColorPicker         颜色选择器(Ctrl / Cmd + Shift + C)
CTags                   
git 

```
