---
title: Windows建立符号链接
published: 2024-12-19
tags: ["Windows"]
lang: zh
abbrlink: symboliclink
---

# Windows建立符号链接

```powershell
MKLINK [[/D] | [/H] | [/J]] Link Target

        /D      创建目录符号链接。默认为文件符号链接。
        /H      创建硬链接而非符号链接。
        /J      创建目录联接。
        Link    指定新的符号链接名称。
        Target  指定新链接引用的路径(相对或绝对)。
```

可解决文件目录空格引起的问题,如下：

Windows对空格充满了深深地恶意。所以在目录前要加个引号。

```powershell
C:\WINDOWS\system32>mklink /D C:\java C:"\Program Files\Java"
```

------
