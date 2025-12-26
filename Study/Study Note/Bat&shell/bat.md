# 目录

[toc]

## 定义

BAT 脚本（也叫批处理脚本）是一种 Windows 平台上的脚本语言，用于批量执行一系列命令。BAT 脚本通常由一系列 DOS 命令和控制结构组成，可以实现自动化的任务处理、系统管理、文件处理等功能。BAT 脚本可以使用 Windows 自带的命令行解释器 cmd.exe 来执行，也可以使用其他第三方解释器，如 PowerShell 等。BAT 脚本的语法和命令与 DOS 命令行界面相同，因此可以很方便地与系统命令和工具进行交互。



## bat 和shell 的区别

BAT 脚本和 Shell 脚本的语法有很大的区别，主要体现在以下几个方面：

1. 命令的语法不同：BAT 脚本中的命令语法通常是基于 DOS 命令的，而 Shell 脚本中的命令语法则是基于 Unix/Linux 命令的。
2. 变量的定义方式不同：在 BAT 脚本中，变量通常使用 `%` 符号来定义和引用，如 `%VAR%`，而在 Shell 脚本中，变量通常使用 `$` 符号来定义和引用，如 `$VAR`。
3. 控制结构的语法不同：BAT 脚本中通常使用 `if`、`for`、`goto` 等关键字来实现控制结构，而 Shell 脚本中则使用 `if`、`for`、`while`、`case` 等关键字来实现控制结构。
4. 路径分隔符不同：在 BAT 脚本中，路径分隔符通常是反斜杠 `\`，而在 Shell 脚本中，路径分隔符通常是正斜杠 `/`。
5. 注释的语法不同：在 BAT 脚本中，注释通常使用 `rem` 关键字或者 `::` 符号，而在 Shell 脚本中，注释通常使用 `#` 符号。



## goto

```bat
@echo off
set /p name=Please enter your name:
echo Hello, %name%!
goto :start

:start
echo This is the start label
goto :end

:end
echo End of script


pause
```

