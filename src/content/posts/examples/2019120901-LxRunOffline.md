---
title: LxRunOffline管理WSL
published: 2024-12-19
tags: ["Windows","WSL"]
lang: zh
abbrlink: lxrunoffline
---

**LxRunOffline**是用于管理Windows Windows子系统（WSL）的功能齐全的实用程序。

- 将任何Linux发行版安装到计算机上的任何目录。
- 将现有安装移动到另一个目录。
- 复制（复制）现有安装。
- 注册现有的安装目录。`这使您可以安装到U盘，并在其他计算机上使用它。`
- 在指定的安装中运行任意Linux命令。
- 配置默认用户，环境变量和[各种标志](https://docs.microsoft.com/zh-cn/windows/win32/api/wslapi/ne-wslapi-wsl_distribution_flags)。
- 将配置导出到XML文件，然后从该文件导入。
- 将安装导出到tar文件。

# Windows 10 子系统Linux重启(不重启Win10)

使用 `PowerShell (Administrator)`

```bash
net stop LxssManager
net start LxssManager
```

# 安装 LxRunOffline

下载解压 [LxRunOffline](https://github.com/DDoSolitary/LxRunOffline) ，并`设置环境变量`。

## LxRunOffline当前版本 (3.4.0) 的选项说明

`l` , `list` - 列出所有已安装的发行版。

`gd` , `get-default` - 获取 bash.exe 使用的默认发行版。

`sd` , `set-default` - 设置 bash.exe 使用的默认发行版。

`i` , `install` - 安装新的发行版。

`sd` , `set-default` - 设置 bash.exe 使用的默认发行版。

`ui` , `uninstall` - 卸载发行版。

`rg` , `register` - 注册现有的安装目录。

`ur` , `unregister` - 取消注册发行版但不删除安装目录。

`m` , `move` - 将发行版移动到新目录。

`d` , `duplicate` - 在新目录中复制现有发行版。

`e` , `export` - 将发行版的文件系统导出到`.tar.gz` 文件，该文件可以通过 `install` 命令安装。

`r` , `run` - 在发行版中运行命令。

`di` , `get-dir` - 获取发行版的安装目录。

`gv` , `get-version` - 获取发行版的文件系统版本。

`ge` , `get-env` - 获取发行版的默认环境变量。

`se` , `set-env` - 设置发行版的默认环境变量。

`ae` , `add-env` - 添加到发行版的默认环境变量。

`re` , `remove-env` - 从发行版的默认环境变量中删除。

`gu` , `get-uid` - 获取发行版的默认用户的 UID。

`su` , `set-uid` - 设置发行版的默认用户的 UID。

`gk` , `get-kernelcmd` - 获取发行版的默认内核命令行。

`sk` , `set-kernelcmd` - 设置发行版的默认内核命令行。

`gf` , `get-flags` - 获取发行版的一些标志。有关详细信息，请参考[这里](https://docs.microsoft.com/zh-cn/windows/win32/api/wslapi/ne-wslapi-wsl_distribution_flags)。

`sf` , `set-flags` - 设置发行版的一些标志。有关详细信息，请参考[这里](https://docs.microsoft.com/zh-cn/windows/win32/api/wslapi/ne-wslapi-wsl_distribution_flags)。

`s` , `shortcut` - 创建启动发行版的快捷方式。

`ec` , `export-config` - 将发行版配置导出到 XML 文件。

`ic` , `import-config` - 从 XML 文件导入发行版的配置。

`sm` , `summary` - 获取发行版的一般信息。

# 使用 LxRunOffline 安装 WSL

与微软商店的安装方式不同，LxRunOf­fline 安装 WSL 更灵活，它可以安装任意发行版到任意目录，还可以自定义 WSL 名称。

如果你没有使用过 WSL ，首先以管理员身份运行 `Pow­er­Shell` ，输入下面的命令开启 “适用于 Linux 的 Win­dows 子系统” 功能，并重启。

```bash
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

- 下载 [WSL 官方离线包](https://docs.microsoft.com/en-us/windows/wsl/install-manual)，改后缀名为`.zip`，解压后可得到名为 `install.tar.gz` 的文件。
- 或者在 [LxRunOffline WiKi](https://docs.microsoft.com/en-us/windows/wsl/install-manual) 中下载大佬们提供的镜像文件。

输入以下命令进行安装：

```bash
lxrunoffline i -n <WSL名称> -d <安装路径> -f <安装包路径>.tar.gz
```

> 注意：加入`-s`参数可在桌面创建快捷方式。

# 使用 LxRunOffline 设置默认用户

当修改过 WSL 的名称或目录后就无法通过[微软官方提供的方法](https://docs.microsoft.com/en-us/windows/wsl/user-support)设置默认用户。这时可以使用 LxRunOf­fline 进行设置。

## 设置普通用户为默认用户

使用 LxRunOf­fline 新安装的 WSL 默认是以 root 用户登录，如果你需要默认以普通用户进行登录，就需要进行下面的操作。

首先运行 WSL ，输入以下命令创建用户：

```bash
useradd -m -s /bin/bash <用户名>
```

然后对该用户设置密码，输入命令后会提示输入两次密码。

```bash
passwd <用户名>
```

授予该用户 sudo 权限。

```bash
usermod -aG sudo <用户名>
```

> 为了保持和微软商店安装的效果一致，这里提及的方法是把用户添加到 sudo 用户组。

查看用户 UID ，一般是 `1000`。

```bash
id -u <用户名>
```

按 `Ctrl`+`D` 退出 WSL ，在 Pow­er­Shell 中输入以下命令：

```bash
lxrunoffline su -n <WSL名称> -v 1000
```

## 设置 root 为默认用户

root 用户的 UID 为 `0`，所以可以直接在 Pow­er­Shell 输入以下命令进行设置：

```none
lxrunoffline su -n <WSL名称> -v 0
```

# 使用 LxRunOffline 转移 WSL 安装目录

LxRunOf­fline 可以对系统中已经安装的 WSL 进行目录转移操作，😂拯救爆满的 C 盘。

查看系统中已安装的 WSL 。

```bash
lxrunoffline l
```

输入命令对 WSL 的目录进行移动。

```bash
lxrunoffline m -n <WSL名称> -d <路径>
lxrunoffline m -n Ubuntu-18.04 -d G:\Ubuntu18.04
```

最后查看路径，进行确认。

```bash
lxrunoffline di -n <WSL名称>
lxrunoffline di -n Ubuntu-18.04
```

# 使用 LxRunOffline 备份和恢复 WSL

使用 LxRunOf­fline 可以方便的对 WSL 进行备份和恢复，同样可以实现转移的操作，而且还可以在转移到其它电脑上。

## 备份 WSL

查看系统中已安装的 WSL 。

```bash
wsl -l
```

然后输入需要备份的 WSL 名称和备份的目标路径。

```bash
lxrunoffline e -n <WSL名称> -f <压缩包路径>.tar.gz
```

> 类似但不等同于`wsl --export  <压缩包路径>.tar`。LxRunOf­fline 备份完会生成一个`.xml`后缀的同名配置文件，比如`WSL.tar.gz.xml`。

## 恢复 WSL

输入以下命令可以恢复已备份的 WSL，和安装是相同的命令。

```bash
lxrunoffline i -n <WSL名称> -d <安装路径> -f <压缩包路径>.tar.gz
```

> 类似但不等同于`wsl --import  <安装路径> <压缩包路径>.tar`。LxRunOf­fline 会读取备份时生成的配置文件并写入配置，前提是同目录且同名。否则你需要加入`-c`参数指定配置文件。

# 使用 LxRunOffline 运行 WSL

和原生运行方式本质上是一样的。

## 创建快捷方式

使用微软应用商店安装的 WSL 会在开始菜单添加应用图标（快捷方式），而使用 LxRunOf­fline 安装 WSL 时可以通过添加 `-s` 参数在桌面创建快捷方式。如果你安装时忘记添加参数，可以使用以下命令进行创建。

```bash
lxrunoffline s -n <WSL名称> -f <快捷方式路径>.lnk
```

## 使用命令运行指定 WSL

在有多个 WSL 的情况下，可以指定运行某个发行版。

```bash
lxrunoffline r -n <WSL名称>
```

> 等同于`wsl -d`

## 设置默认 WSL

设置默认 WSL 后，可以在 `cmd` 和 `powershell` 中输入 `wsl` 直接调用默认的 WSL 。

```bash
lxrunoffline sd -n <WSL名称>
```

> 等同于`wsl -s`

# 使用 LxRunOffline 修改 WSL 名称

查看 WSL 名称。

```bash
wsl -l
```

查看 WSL 安装目录。

```bash
lxrunoffline di -n <WSL名称>
```

导出指定的 WSL 配置文件到目标路径。

```bash
lxrunoffline ec -n <WSL名称> -f <配置文件路径>.xml
```

> 配置信息可以输入`lxrunoffline sm -n`查看

取消注册（这个操作不会删除目录）

```bash
lxrunoffline ur -n <WSL名称>
```

使用新名称注册

```bash
lxrunoffline rg -n <WSL名称> -d <WSL路径> -c <配置文件路径>.xml
```

📖[参考](https://github.com/DDoSolitary/LxRunOffline)

------
