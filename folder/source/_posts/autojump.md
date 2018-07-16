---
title: autojump
date: 2016/12/12 18:52
tags: tools
categories: 工具类
---

## mac安装autojump

    autojump是一个命令行工具，它可以使用快捷命令，直接跳转到配置好的目录，而不用管现在身在何处。  

1. 安装zsh：
    `sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
 <!-- more -->
2. 将zsh设置成默认的shell：`chsh -s /bin/zsh` (重启shell)
3. `echo $SHELL`可以查看用的哪个shell（bash or zsh）
4. 安装autojump：`brew install autojump`（确保有brew）
5. 使用`vim .zshrc`打开.zshrc（有些人会找不到.zshrc这个文件，其实安装了zsh才会有.zshrc ，在默认打开的终端目录下。可以打开终端并且ls -a查看）。
    * 找到 plugins=，在后面添加autojump：`plugins=(git autojump)`
    * 新开一行，添加：`[[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh`
    * `：wq`保存退出
6. 重启终端，autojump就可以使用了，例如：
      添加一条快捷键：`j -a s '/Users/XXX/Desktop/code/shark’`（j -a 你定义的快捷命令 ‘需要跳转的目录位置’）

      进入shark：`j s`

##### [转自] [mac安装autojump](https://my.oschina.net/luweiweiwei/blog/804679)