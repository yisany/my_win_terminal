# Win10 Terminal 打造

## 目录

- [Win10 Terminal 打造](#win10-terminal-%E6%89%93%E9%80%A0)
  - [目录](#%E7%9B%AE%E5%BD%95)
  - [0. 软件选型](#0-%E8%BD%AF%E4%BB%B6%E9%80%89%E5%9E%8B)
  - [1. 软件安装](#1-%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85)
    - [1.1. 安装Git](#11-%E5%AE%89%E8%A3%85git)
    - [1.2. 安装Windows Terminal](#12-%E5%AE%89%E8%A3%85windows-terminal)
    - [1.3. 获取相关配置文件](#13-%E8%8E%B7%E5%8F%96%E7%9B%B8%E5%85%B3%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
  - [2. 终端设置](#2-%E7%BB%88%E7%AB%AF%E8%AE%BE%E7%BD%AE)
    - [2.1. Git 设置](#21-git-%E8%AE%BE%E7%BD%AE)
      - [2.1.1. 安装字体](#211-%E5%AE%89%E8%A3%85%E5%AD%97%E4%BD%93)
      - [2.1.2. 安装主题](#212-%E5%AE%89%E8%A3%85%E4%B8%BB%E9%A2%98)
      - [2.1.3. 安装拓展命令](#213-%E5%AE%89%E8%A3%85%E6%8B%93%E5%B1%95%E5%91%BD%E4%BB%A4)
      - [2.1.4. 配置alias](#214-%E9%85%8D%E7%BD%AEalias)
    - [2.2. Windows Terminal 设置](#22-windows-terminal-%E8%AE%BE%E7%BD%AE)
  - [3. 其他](#3-%E5%85%B6%E4%BB%96)
    - [3.1. VS Code 使用 Git](#31-vs-code-%E4%BD%BF%E7%94%A8-git)
    - [3.2. Terminal 快捷键唤出](#32-terminal-%E5%BF%AB%E6%8D%B7%E9%94%AE%E5%94%A4%E5%87%BA)
  - [4. 参考文章](#4-%E5%8F%82%E8%80%83%E6%96%87%E7%AB%A0)
  - [5. Update](#5-update)

## 0. 软件选型

文档的目的在于探究在win10系统下打造一个好用的Terminal终端系统。以目前Win10版本（1903）的为基准，其自带的`CMD`以及`PowerShell`还是使用起来非常不便，例如不支持Linux的常用命令， 不支持多标签页等。

随着Windows Terminal和WSL2的发布， Win10上已经拥有了比之前更好的一套终端解决方案，但是目前的WSL2使用起来还是资源消耗太高，不适合8G（包含8G）以下的配置使用。

自己目前的方案是：

- 终端： Windows Terminal

  Windows Terminal 能够提供优秀的多标签，分屏功能；

- Shell：Git Bash

  Git Bash能够支持绝大多数的Linux命令并且支持alias，且性能优秀；

## 1. 软件安装

### 1.1. 安装Git

在官方网站下载Git的安装包

[Git Bash](https://git-scm.com/downloads)

### 1.2. 安装Windows Terminal

目前微软只给1903及以上Win10版本适配了Windows Terminal, 低于这个版本的Win10无法安装。

在Win10自带的软件商店里搜索`Windows Terminal`根据提示安装即可

### 1.3. 获取相关配置文件

目前相关的配置文件存放在GitHub仓库，使用Git命令来进行获取，创建一个文件夹用来存放配置（不要放在桌面，纯英文路径）。

```bash
$ git clone https://github.com/yisany/my_win_terminal.git
$ cd my_win_terminal
```

## 2. 终端设置

分为两个部分：Git Bash & Windows Terminal

### 2.1. Git 设置

以下操作皆在刚刚下载的配置文件文件夹下操作

#### 2.1.1. 安装字体

Git自带的字体会导致Unicode字符乱码问题，需要替换字体。执行命令：

```bash
$ start c://Windows//Fonts && start %cd%/fonts*
```

<p align="center">
    <img alt="Git Bash" src="https://user-images.githubusercontent.com/38936252/54868439-70ee3200-4dc7-11e9-9096-d0159d78ea3c.gif" width="750">
</p>

#### 2.1.2. 安装主题

安装主题后同时会开启复制粘贴快捷键：Ctrl + Shift + C/V，需要 Git Bash 版本大于 2.20.0 才可以使用。

```bash
$ cp .minttyrc ~ && cp git-prompt.sh /etc/profile.d
```

<p align="center">
    <img alt="Git Bash" src="https://user-images.githubusercontent.com/38936252/54868400-09d07d80-4dc7-11e9-8498-b6f146133b8c.gif" width="750">
</p>

#### 2.1.3. 安装拓展命令

支持wget和tree命令

```bash
$ cp tools/* /usr/bin
```

#### 2.1.4. 配置alias

```bash
$ cp .bash_profile ~
```

### 2.2. Windows Terminal 设置

这个配置比较简单，是json格式的， 提供一份我自己的配置，使用Git作为默认终端。

```bash
$ cat profiles.json
```

## 3. 其他

### 3.1. VS Code 使用 Git

在 VSCode 中使用 `Git Bash` 只需要在 `Settings.json` 中添加如下两行即可，第一行中 `bash.exe` 的文件路径需要改成自己的，第二行是非必须配置，不配置无法使用 `alias`。

```
{
  "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": ["--login", "-i"]
}
```

### 3.2. Terminal 快捷键唤出

1. 打开`terminal_shorcutwe`文件夹，运行`wt.reg`注册表：

   > 自己修改路径: D:\\workplace\\my_win_terminal\\terminal_shorcutwe

   ```
   Windows Registry Editor Version 5.00
    
   [HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
   @="Windows terminal here"
   "Icon"="D:\\workplace\\my_win_terminal\\terminal_shorcutwe\\wt_32.ico"
    
   [HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
   @="D:\\workplace\\my_win_terminal\\terminal_shorcutwe\\wt.exe"
   ```

2. 开Windows Terminal 的配置文件`profiles.json`, 找到`startingDirectory`，改成null：

   ```json
   "startingDirectory": null
   ```

## 4. 参考文章

[My Git Bash](https://github.com/xnng/my-git-bash)

[配置Windows Terminal在任意目录打开的方法](https://blog.csdn.net/weixin_43870742/article/details/100830921)

[Windows Terminal 安装及美化](https://www.cnblogs.com/KiraYoshikage/p/11443741.html)

## 5. Update

- 2020-02-28

  第一次初始化









