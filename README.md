# 我的 dwm 配置

dwm 是 X 服务的一个非常轻量的、快速的动态窗口管理器。

<!-- vim-markdown-toc GFM -->

* [安装前的准备](#安装前的准备)
* [安装](#安装)
* [运行](#运行)
    * [使用登录管理器启动 dwm](#使用登录管理器启动-dwm)
    * [使用 startx 启动 dwm](#使用-startx-启动-dwm)
* [配置](#配置)
* [补丁](#补丁)
* [使用方法](#使用方法)
    * [0 前置知识](#0-前置知识)
        * [0.1 一些键位](#01-一些键位)
        * [0.2 桌面和标签](#02-桌面和标签)
        * [0.3 状态栏](#03-状态栏)
    * [1 键盘快捷键](#1-键盘快捷键)
        * [1.1 移动焦点](#11-移动焦点)
        * [1.2 关于桌面和标签](#12-关于桌面和标签)
        * [1.3 打开软件](#13-打开软件)
        * [1.4 更改窗口布局](#14-更改窗口布局)
        * [1.5 关于声音的控制](#15-关于声音的控制)
        * [1.6 关于窗口之间的缝隙](#16-关于窗口之间的缝隙)
        * [1.7 其他功能](#17-其他功能)
    * [2 鼠标点击](#2-鼠标点击)
        * [2.1 更改窗口布局](#21-更改窗口布局)
        * [2.2 打开软件](#22-打开软件)
        * [2.3 关于桌面和标签](#23-关于桌面和标签)

<!-- vim-markdown-toc -->

## 安装前的准备

- 你需要有 `Xlib` 头文件。  
- 你最好拥有 `picom` 或其他窗口渲染器，并在 `scripts` 文件夹中的 `autostart.sh` 脚本中启动它。  
- 你最好拥有 [Nerd-Fonts](https://github.com/ryanoasis/nerd-fonts) 字体，因为状态栏的脚本需要用到这些字体。  
- 更改 `config.def.h` 或 `config.h` 中的设置以符合你的喜好。  
- 更改 `scripts` 文件夹中的 `autostart.sh` 脚本（即开机启动项），以符合你的要求。  
- 更改所有文件中的路径以符合你的电脑上的路径（默认的安装路径为 `~/Programs/Softwares/dwm` 目录下，默认的壁纸路径为 `~/Pictures/Wallpapers` 路径下）。  
- 我的 dwm 需要的软件：
    - [我的 st](https://github.com/LogicSkky/my-st)
    - [我的 dmenu](https://github.com/LogicSkky/my-dmenu)
    - feh
    - amixer
    - flameshot
    - google-chrome
    - picom
## 安装

（以安装在 `~/Programs/Softwares/dwm` 路径为例）

- 进入相应的目录：

```
cd ~/Programs/Softwares
```

- 克隆这个仓库：

```
git clone https://github.com/logicskky/dwm.git
```

- 进入这个文件夹：

```
cd dwm
```

- 编辑 `config.mk` 这个文件来匹配你的本地设置（dwm 默认安装到 `/usr/local` 命名空间下）。  
- 运行以下命令来编译和安装 dwm（可能需要作为 root 用户来执行命令）：  

```
make clean install
```

## 运行

### 使用登录管理器启动 dwm

把 `others` 文件夹里的 `dwm.desktop` 复制到 `/usr/share/xsessions` 这个文件夹下，之后在登录管理器选择启动 dwm 即可。

### 使用 startx 启动 dwm

把下面这一行添加到你的 `.xinitrc` 中，以使用 startx 来启动 dwm。  

```
exec dwm
```

为了将 dwm 连接到一个特定的显示器，请确保 DISPLAY 环境变量设置正确，例如：  

```
DISPLAY=foo.bar:1 exec dwm
```

（这将在主机 foo.bar 的显示器 :1 上启动 dwm）。  

为了在状态栏中显示信息，你可以在 `.xinitrc` 中这样启动 dwm（不过我的 dwm 会自动启动一个控制状态栏的脚本，所以不需要这样启动）：

```
while xsetroot -name "`date` `uptime | sed 's/.*,//'`"
do
	sleep 1
done &
exec dwm
```

## 配置

Dwm 的配置是通过自定义 `config.h` 和重新编译安装来实现的。  
不过我推荐你自定义 `config.def.h` 这个文件，但要注意，编译安装之前要先删除 `config.h` 这个文件，然后安装完成后，会自动生成 `config.h` 这个文件。  

## 补丁

这些补丁的具体作用详见 [这里](https://github.com/LogicSkky/my-dwm/tree/master/patches) 。

- [alphasystray.diff](https://github.com/theniceboy/dwm/blob/master/patches/alphasystray.diff)
- [dwm-autostart-20161205-bb3bd6f.diff](https://dwm.suckless.org/patches/autostart/)
- [dwm-awesomebar-20191003-80e2a76.diff](https://dwm.suckless.org/patches/awesomebar/)
- [dwm-fullscreen-6.2.diff](https://dwm.suckless.org/patches/fullscreen/)
- [dwm-hide_vacant_tags-6.2.diff](https://dwm.suckless.org/patches/hide_vacant_tags/)
- [dwm-noborder-6.2.diff](https://dwm.suckless.org/patches/noborder/)
- [dwm-pertag-20170513-ceac8c9.diff](https://dwm.suckless.org/patches/pertag/)
- [dwm-rotatestack-20161021-ab9571b.diff](https://dwm.suckless.org/patches/rotatestack/)
- [dwm-scratchpad-6.2.diff](https://dwm.suckless.org/patches/scratchpad/)
- [dwm-vanitygaps-20190508-6.2.diff](https://dwm.suckless.org/patches/vanitygaps/)

## 使用方法

### 0 前置知识

#### 0.1 一些键位  

`Mod` 键为 `Windows` 键；  
`Space` 键为空格键；  
`<number>` 键为除 `0` 外的任意一个数字键。  

#### 0.2 桌面和标签  

dwm 下的桌面其实并不是真正的桌面，而是显示打了某一个标签的某些窗口。  

假设我的电脑上有五个窗口，分别为 `google-chrome`，`st`，`NeoVim`，`Ranger`，`htop`。  
其中，每个窗口都打上了标签：

| 窗口                    | 标签 |
|-------------------------|------|
| `google-chrome` 和 `st` | `1`  |
| `NeoVim`                | `3`  |
| `Ranger` 和 `htop`      | `6`  |

那么，如果我切换到 `1` 号桌面，那么实际上就是显示打了 `1` 这个标签的窗口，即为显示 `google-chrome` 和 `st` 这两个窗口。  
接下来，我又给某些窗口增加了一些标签：

| 窗口                    | 标签       |
|-------------------------|------------|
| `google-chrome` 和 `st` | `1`        |
| `NeoVim`                | `3` 和 `5` |
| `Ranger` 和 `htop`      | `6` 和 `5` |

那么在现在，如果我切换到 `5` 号桌面，实际上就是显示打了 `5` 这个标签的窗口，即为显示 `NeoVim`、`Ranger`和`htop`。  
但需要注意的是，由于这三个窗口都各打了两个标签，所以在别的相应的桌面也能看到这些窗口，如切换到 `3` 号桌面也会显示 `NeoVim` 这个窗口。  

#### 0.3 状态栏
dwm 的状态栏显示的信息可以通过以下命令进行定制：

```
xsetroot -name "Hello"
```

这将在状态栏显示 `Hello`。

所以，我们可以通过一个脚本来定时刷新状态栏显示的信息。

我的 dwm 的状态栏由 5 个部分组成：

```
+-----------------------------------------------------------------------------+
|   A   |  B  |           C            |              D             |    E    |
+-----------------------------------------------------------------------------+
```

- A：显示当前有窗口的桌面的标签；
- B：显示当前桌面的窗口管理模式；
- C：显示当前桌面的所有窗口的名称；
- D：我自己定制的状态栏所显示的信息；
- E：显示系统托盘。

### 1 键盘快捷键

#### 1.1 移动焦点

| 快捷键  | 作用               |
|---------|--------------------|
| `Mod+k` | 往上（左）移动焦点 |
| `Mod+j` | 往下（右）移动焦点 |

#### 1.2 关于桌面和标签

| 快捷键                    | 作用                                                 |
|---------------------------|------------------------------------------------------|
| `Mod+Tab`                 | 切换到上一次浏览的桌面                               |
| `Mod+<number>`            | 切换到某一个桌面                                     |
| `Mod+Ctrl+<number>`       | 将某一个桌面的窗口和当前桌面的窗口一起浏览           |
| `Mod+0`                   | 将全部桌面的窗口一起浏览                             |
| `Mod+Shift+<number>`      | 用某个标签替换该窗口原来的标签（将窗口移至某个桌面） |
| `Mod+Ctrl+Shift+<number>` | 给某个窗口增加某个标签                               |
| `Mod+Shift+0`             | 给某个窗口增加全部的标签                             |

#### 1.3 打开软件

| 快捷键       | 作用                 |
|--------------|----------------------|
| `Mod+Return` | 打开 `st`            |
| `Mod+d`      | 打开 `dmenu`         |
| `Mod+c`      | 打开 `Google-Chrome` |

#### 1.4 更改窗口布局

| 快捷键             | 作用                                       |
|--------------------|--------------------------------------------|
| `Mod+Shift+t`      | 切换到平铺模式（`Tile`）                   |
| `Mod+Shift+f`      | 切换到浮动模式（`Float`）                  |
| `Mod+Shift+m`      | 切换到单页模式（`Monocle`）                |
| `Mod+f`            | 进入进入全屏模式                           |
| `Mod+Space`        | 切换到上一种窗口摆放方式                   |
| `Mod+Shift+Space`  | 将当前窗口切换到浮动模式/平铺模式          |
| `Mod+Shift+k`      | 将窗口往上（左）移动                       |
| `Mod+Shift+j`      | 将窗口往下（右）移动                       |
| `Mod+o`            | 将窗口横向分割                             |
| `Mod+p`            | 将窗口纵向分割                             |
| `Mod+h`            | 将窗口的纵向分割线左移                     |
| `Mod+l`            | 将窗口的纵向分割线右移                     |
| `Mod+Shift+Return` | 将当前窗口变成主窗口，或者放到栈区域的顶部 |

#### 1.5 关于声音的控制

| 快捷键        | 作用          |
|---------------|---------------|
| `Mod+Shift+w` | 把声音升高 5% |
| `Mod+Shift+s` | 把声音降低 5% |
| `Mod+Shift+e` | 打开/关闭声音 |

#### 1.6 关于窗口之间的缝隙

**注：`1` 表示窗口与窗口之间，`2` 表示窗口与显示屏边缘之间。**
| 快捷键            | 作用                                     |
|-------------------|------------------------------------------|
| `Mod+Alt+0`       | 打开/关闭 `1` 和 `2` 的缝隙              |
| `Mod+Alt+Shift+0` | 把 `1` 和 `2` 之间的缝隙切换到默认的大小 |
| `Mod+Alt+h`       | 放大 `1` 和 `2` 的缝隙                   |
| `Mod+Alt+l`       | 缩小 `1` 和 `2` 的缝隙                   |
| `Mod+Alt+Shift+h` | 放大 `2` 的缝隙                          |
| `Mod+Alt+Shift+l` | 缩小 `2` 的缝隙                          |
| `Mod+Alt+Ctrl+h`  | 放大 `1` 的缝隙                          |
| `Mod+Alt+Ctrl+l`  | 缩小 `1` 的缝隙                          |
| `Mod+u`           | 放大 `1` 的横向的窗口分割缝隙            |
| `Mod+i`           | 缩小 `1` 的横向的窗口分割缝隙            |
| `Mod+Ctrl+u`      | 放大 `1` 的纵向的窗口分割缝隙            |
| `Mod+Ctrl+i`      | 缩小 `1` 的纵向的窗口分割缝隙            |
| `Mod+Alt+u`       | 放大 `2` 的横向的缝隙                    |
| `Mod+Alt+i`       | 缩小 `2` 的横向的缝隙                    |
| `Mod+Shift+u`     | 放大 `2` 的纵向的缝隙                    |
| `Mod+Shift+i`     | 缩小 `2` 的纵向的缝隙                    |

#### 1.7 其他功能

| 快捷键             | 作用                      |
|--------------------|---------------------------|
| `Mod+'`            | 打开/关闭 `scratchpad`    |
| `Mod+b`            | 打开/关闭状态栏           |
| `Mod+Shift+d`      | 更换壁纸                  |
| `Mod+Shift+a`      | 打开 `flameshot` 进行截图 |
| `Mod+Ctrl+q`       | 关闭当前窗口              |
| `Mod+Ctrl+Shift+c` | 关闭 `dwm`                |
| `Mod+,`            | 暂不了解该快捷键的功能    |
| `Mod+.`            | 暂不了解该快捷键的功能    |
| `Mod+Shift+,`      | 暂不了解该快捷键的功能    |
| `Mod+Shift+.`      | 暂不了解该快捷键的功能    |

### 2 鼠标点击

**注：这里的 `A` / `B` / `C` / `D` / `E` 所代表的部分详见 [这里](#03-状态栏)。**

#### 2.1 更改窗口布局

| 鼠标动作                 | 作用                                                 |
|--------------------------|------------------------------------------------------|
| `左键状态栏上的 B`       | 切换到上一种窗口摆放方式                             |
| `右键状态栏上的 B`       | 切换到浮动模式（`Float`）                            |
| `左键状态栏上的 C`       | 将焦点移至该窗口，或隐藏/显示该窗口                  |
| `中键状态栏上的 C`       | 将当前焦点所在的窗口变成主窗口，或者放到栈区域的顶部 |
| `Mod+左键窗口并移动光标` | 将当前窗口变为浮动窗口，并随鼠标移动而移动           |
| `Mod+中键窗口`           | 将当前窗口变为浮动窗口或取消浮动                     |
| `Mod+右键窗口并移动光标` | 将当前窗口变为浮动窗口，并随鼠标的移动而改变大小     |

#### 2.2 打开软件

| 鼠标动作           | 作用      |
|--------------------|-----------|
| `中键状态栏上的 D` | 打开 `st` |

#### 2.3 关于桌面和标签

| 鼠标动作               | 作用                                                 |
|------------------------|------------------------------------------------------|
| `左键状态栏上的 A`     | 切换到某一个桌面                                     |
| `右键状态栏上的 A`     | 将某一个窗口和当前窗口一起浏览                       |
| `Mod+左键状态栏上的 A` | 用某个标签替换该窗口原来的标签（将窗口移至某个桌面） |
| `Mod+右键状态栏上的 A` | 给某个窗口增加某个标签                               |

