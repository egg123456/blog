---
title: registry
date: 2018/5/14
categories:
- OS
---
> 注册表（Registry，繁体中文版Windows操作系统称之为登录档案）是Microsoft Windows中的一个重要的数据库，用于存储系统和应用程序的设置信息.

#### 注册表的数据结构
注册表由项（也叫主键或称“键”）、子项（子键）和值构成。一个项就是分支中的一个文件夹，而子项就是这个文件夹当中的子文件夹，子项同样它也是一个项。一个值则是一个项的当前定义，由名称、数据类型以及分配的值组成。一个项可以有一个或多个值，每个值的名称各不相同，如果一个值的名称为空，则该值为该项的默认值。

#### 注册表配置之打开vscode
```reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\vscode]
@="URL:VSCode Protocol"
"URL Protocol"=""

[HKEY_CLASSES_ROOT\vscode\shell]

[HKEY_CLASSES_ROOT\vscode\shell\open]

[HKEY_CLASSES_ROOT\vscode\shell\open\command]
@=""D:\VScode\Microsoft VS Code\Code.exe" "%1""

```
代码解释
1. Windows Registry Editor Version 5.00 这行表明该文件是一个 Windows 注册表编辑器文件，这是标准的头部，用于告诉 Windows 如何解析文件。
2. [HKEY_CLASSES_ROOT\vscode] 这是一个注册表键的开始。在这里，\vscode 表示创建一个名为 vscode 的新键。
3. @="URL:VSCode Protocol" 在 vscode 键下，这行设置了默认值（表示为 @ ），通过 "URL:VSCode Protocol" 对这个键进行描述。
4. "URL Protocol"="" 这行是设置一个名为 URL Protocol 的空字符串值。这是代表这个新键是一个 URI 协议。
5. [HKEY_CLASSES_ROOT\vscode\shell] 创建一个名为 shell 的子键，这是一个固定键，代表GUI界面的处理。
6. [HKEY_CLASSES_ROOT\vscode\shell\open] 在 shell 下创建一个名为 open 的子键。这耶是一个固定键，open 是一个标准动作，用来执行打开操作。
7. [HKEY_CLASSES_ROOT\vscode\shell\open\command] 在 open 下创建一个名为 command 的子键。这是一个固定键，指定了当协议被触发时要执行命令。
8. @=""D:\VScode\Microsoft VS Code\Code.exe" "%1"" 在 command 键下，设置默认值为 VSCode 的路径。 "%1" 是一个占位符，用于表示传递给协议的任何参数，这里并无实际用处。

在windows注册表编辑器中显示为：
+ vscode
  + shell
    + open
      + command

使用时，浏览器地址栏输入  vscode://open 即可打开 vscode 应用程序
