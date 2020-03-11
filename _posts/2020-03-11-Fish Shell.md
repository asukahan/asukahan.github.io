---

layout:     post
title:      Fish Shell 介绍
subtitle:   一个好用的Shell
date:       2020-03-11
author:     Asukahan
header-img: img/abstract-4626114_1920.jpg
catalog: true
tags:
    - Linux
    - Mac

---



![fish shell](https://www.tecmint.com/wp-content/uploads/2015/07/Fish-Shell-for-Linux.png)


作为系统维护人员或是程序员，命令行是必备技能。图形界面虽然更直观，但也妥协了效率，命令行界面更绝对并且提供了更高效直接的操作方式。


## 简介
Fish 是" the friendly interactive shell "的简称，最大特点就是方便易用。很多其他 Shell 需要配置才有的功能，Fish 默认提供，不需要任何配置。如果你想拥有一个方便好用的 Shell，又不想学习一大堆语法，或者花费很多时间配置，那么你一定要尝试一下 Fish。

![](http://47.105.183.69/img/post-fishshell/fishshell.png)

## 安装
Ubuntu 和 Debian 的安装方法。
```
$ sudo apt-get install fish
```

Mac 的安装方法。
```
$ brew install fish
```

其他系统的安装请参考[官方网站](https://fishshell.com/)。

## 启动与帮助
安装完成后，就可以启动 Fish。

```
$ fish
```

由于 Fish 的语法与 Bash 有很大差异，Bash 脚本一般不兼容。因此，我建议不要将 Fish 设为默认 Shell，而是每次手动启动它。

使用过程中，如果需要帮助，可以输入help命令。浏览器就会自动打开，显示在线文档。

```
$ help
```
## 彩色显示
进入 Fish 以后，你注意到的第一件事，可能就是它默认彩色显示。

+ 无效命令为红色
+ 有效命令为蓝色
+ 有效路径会有下划线。

![](http://47.105.183.69/img/post-fishshell/colourdisplay.png)

## 自动建议

Fish 会自动在光标后面给出建议，表示可能的选项，颜色为灰色。

如果采纳建议，可以按下`→`或`Control + F`。如果只采纳一部分，可以按下`Alt + →`。

## 自动补全
输入命令时，Fish 会自动显示匹配的上一条历史记录。
```
$ git commit -m "feat: first commit"
```

如果没有匹配的历史记录，Fish 会猜测可能的结果，自动补全各种输入。比如，输入pyt再按下Tab，就会自动补全为python命令。

如果有多个可能的结果，Fish 会把它们都列出，还带有简要介绍。

```
$ vi[按下 Tab 键]

vi (Executable link, 2.7MB)
view (Vi IMproved, 一个程序员的文本编辑器)
viewer.py (Executable, 967B)
viewres  (Graphical class browser for Xt)
...and 12 more rows
```

这时，再按一次tab，就可以在这些命令之中选择。

除了补全命令，Fish 还可以补全参数。比如，ls命令的-l参数后面按下Tab键，就会显示可以连用的其他参数。

```
$ ls -l[按下 Tab 键]

-l1  (List one file per line)
-lA  (Show hidden except . and ..)  
-la  (Show hidden)
-lB  (Ignore files ending with ~)
...and 16 more rows
```
Fish 还可以自动补全 Git 分支。

## 易懂的语法
Fish 的语法非常自然，一眼就能看懂。

+ if语句
```
if grep fish /etc/shells
    echo Found fish
else if grep bash /etc/shells
    echo Found bash
else
    echo Got nothing
end
```


+ switch语句
```
switch (uname)
case Linux
    echo Hi Tux!
case Darwin
    echo Hi Hexley!
case FreeBSD NetBSD DragonFly
    echo Hi Beastie!
case '*'
    echo Hi, stranger!
end
```


+ while循环
```
while true
    echo "Loop forever"
end
```


+ for循环
```
for file in *.txt
    cp $file $file.bak
end
```

## 函数
Fish 的函数用来封装命令，或者为现有的命令起别名。

```
function ll
    ls -lhG $argv
end
```
上面代码定义了一个ll函数。命令行执行这个函数以后，就可以用ll命令替代ls -lhG。其中，变量\$argv表示函数的参数。

下面是另一个例子。

```
function ls
    command ls -hG $argv
end
```
上面的代码重新定义ls命令。注意，函数体内的ls之前，要加上command，否则会因为无限循环而报错。

## 提示符
fish_prompt函数用于定义命令行提示符（prompt）。

```
function fish_prompt
    set_color purple
    date "+%m/%d/%y"
    set_color FF0
    echo (pwd) '>'
    set_color normal
end
```

执行上面的函数以后，你的命令行提示符就会变成下面这样。

```
02/06/13
/home/tutorial > 
```

## 配置
Fish 的配置文件是

```
~/.config/fish/config.fish
```
每次 Fish 启动，就会自动加载这个文件。

我们可以在这个文件里面写入各种自定义函数，它们会被自动加载。比如，上面的fish_prompt函数就可以写在这个文件里面，这样每次启动 Fish，就会出现自定义的提示符。

Fish 还提供 Web 界面配置该文件。

```
$ fish_config
```

输入上面的命令以后，浏览器就会自动打开本机的 8000 端口，用户可以在网页上对 Fish 进行配置，比如选择提示符和配色主题。

> 引用：http://www.ruanyifeng.com/blog/2017/05/fish_shell.html
