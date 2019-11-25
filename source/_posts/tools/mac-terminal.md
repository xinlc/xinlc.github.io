---
layout: post
title: Mac Terminal 配置
date: 2017-07-03 15:30:00 +0800
categories: 工欲善其事必先利其器
tags:
  - linux
---

## [iTerm2](https://www.iterm2.com/downloads.html)

### 安装 zsh

```bash
brew install zsh

zsh --version

# 将zsh设置为默认的Shell。
chsh -s /bin/zsh
```

### 安装 oh my zsh

```bash
# 安装
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# 卸载
uninstall_oh_my_zsh
```

## 常用快捷键

- `Ctrl + a`：移到命令行首
- `Ctrl + e`：移到命令行尾
- `Ctrl + f`：按字符前移（右向）
- `Ctrl + b`：按字符后移（左向）
- `Alt + f`：按单词前移（右向）
- `Alt + b`：按单词后移（左向）
- `Ctrl + p`：历史中的上一条命令, 或者 文本中移动到上一行
- `Ctrl + n`：历史中的下一条命令,或者 文本中移动到下一行
- `Ctrl + r`：往后搜索历史命令
- `Ctrl + s`：往前搜索历史命令
- `Ctrl + g`：从历史搜索模式退出
- `Alt + .`：使用上一条命令的最后一个参数
- `Ctrl + xx`：在命令行首和光标之间移动
- `Ctrl + t`：将光标位置的字符和前一个字符进行位置交换
- `Ctrl + d`：删除一个字符,删除一个字符，相当于通常的Delete键
- `Ctrl + h`：退格删除一个字符,相当于通常的Backspace键
- `Ctrl + w`：从光标处删除至字首
- `Ctrl + u`：从光标处删除至命令行首
- `Ctrl + k`：从光标处删除至命令行尾
- `Ctrl + l`：清屏, 类似 clear 命令效果
- `Alt + d`：从光标处删除至字尾
- `Ctrl + d`：删除光标处的字符
- `Ctrl + y`：粘贴由 Ctrl+u ， Ctrl+d ， Ctrl+w 删除的单词
- `Ctrl + &`：恢复 ctrl+h 或者 ctrl+d 或者 ctrl+w 删除的内容
- `Ctrl + c`：终止进程/命令
- `Alt + c`：从光标处更改为首字母大写的单词
- `Ctrl + z`：挂起命令
- `Alt + u`：从光标处更改为全部大写的单词
- `Alt + l`：从光标处更改为全部小写的单词
- `Ctrl + t`：交换光标处和之前的字符
- `Alt + t`：交换光标处和之前的单词
- `Alt + Backspace`：与 `Ctrl + w` 相同，分隔符有些差别
- `Ctrl + o`：执行当前命令，并选择上一条命令

## Bang (!) 命令

- `!!`：执行上一条命令
- `!blah`：执行最近的以 blah 开头的命令，如 !ls
- `!blah:p`：仅打印输出，而不执行
- `!$`：上一条命令的最后一个参数，与 Alt + . 相同
- `!$:p`：打印输出 !$ 的内容
- `!*`：上一条命令的所有参数
- `!*:p`：打印输出 !* 的内容
- `^blah`：删除上一条命令中的 blah
- `^blah^foo`：将上一条命令中的 blah 替换为 foo
- `^blah^foo^`：将上一条命令中所有的 blah 都替换为 foo