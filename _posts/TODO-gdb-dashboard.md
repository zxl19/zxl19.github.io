---
layout: post
title: 使用gdb-dashboard配置GDB调试界面
date: TODO
author: zxl19
tags: [C++, GDB, Note]
comments: true
toc: true
pinned: false
---

使用gdb-dashboard配置GDB调试界面。

<!-- more -->

## 安装

gdb-dashboard只包含一个`.gdbinit`脚本，直接下载到主目录即可：

```shell
wget -P ~ https://git.io/.gdbinit
```

## 配置

### 脚本中配置

#### 关闭保存历史命令

```text
set history save off
```

#### 添加项目路径

将自己的项目路径添加到`~/.gdbinit`文件中：

```text
add-auto-load-safe-path /path/to/my/projects/.gdbinit
```

或者直接添加根目录（不建议）：

```text
add-auto-load-safe-path /
```

#### 重新定义GDB的continue语句

为避免continue语句引起的bug，重新定义`.gdbinit`文件中：

```text
define continue-breakpoint
python gdb.post_event(lambda: gdb.execute('continue'))
end
```

### GDB中配置

#### 常用命令

查看帮助

```shell
help dashboard
```

打开/关闭gdb-dashboard

```shell
dashboard -enabled [on/off]
```

配置

```shell
dashboard -layout
```

```shell
Dashboard    (default TTY)

assembly     (default TTY)
breakpoints  (default TTY)
expressions  (default TTY)
history      (default TTY)
memory       (default TTY)
registers    (default TTY)
source       (default TTY)
stack        (default TTY)
threads      (default TTY)
variables    (default TTY)
```

#### 修改高亮方案

查看：

```shell
dashboard -style syntax_highlighting
```

设置：

```shell
dashboard -style syntax_highlighting 'monokai'
```

```shell
python
from pygments.styles import *
for style in get_all_styles():
    command = 'dashboard -style syntax_highlighting {!r}'.format(style)
    gdb.execute(command)
    print(command)
    if input('Use this style? (y/N) ') == 'y':
        break
end
```

```shell
python
from pygments.styles import *
for style in get_all_styles():
    command = 'dashboard -style syntax_highlighting {!r}'.format(style)
    gdb.execute(command)
    print(command)
    if input('Use this style? (y/N) ') == 'y':
        break
end
```

## 参考

1. [神仙GDB调试工具gdb-dashboard-电子的文章-知乎](https://zhuanlan.zhihu.com/p/435918702)
2. [cyrus-and/gdb-dashboard](https://github.com/cyrus-and/gdb-dashboard)
