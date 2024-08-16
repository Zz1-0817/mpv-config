# MPV 配置笔记

## 配置文件

对于配置文件方面, 可参考的主要资料为 [mpv/files](https://mpv.io/manual/stable/#files):

- mpv 配置文件位置: 本段下面文字均 **仅** 对 Windows 系统而言, 默认配置文件位置应在为`%APPDATA%/mpv` 下(如果使用如 "scoop" 之类的软件下载 mpv 则会有所不同).
    例如`%APPDATA%/mpv/mpv.conf`.
    如果存在目录名为 `portable_config` 位于 `mpv` 可执行文件, 即 `mpv.exe` 同级目录下, 则只会加载此目录下的配置.
    同时 **watch later** 文件 和 **缓存** 均会写入此目录中.
- mpv 配置文件加载顺序(Linus 平台)
        - `/usr/local/etc/mpv/mpv.conf`
        - `~/.cache/mpv`
        - `~/.config/mpv`
        - `~/.mpv/`
        - `~/.config/mpv/mpv.conf`
        - `~/.config/mpv/input.conf`
        - `~/.config/mpv/fonts.conf`
        - `~/.config/mpv/subfont.ttf`
        - `~/.config/mpv/scripts/` 此目录下文件按字典序加载
        - `~/.local/state/mpv/watch_later`
        - `~/.config/mpv/script-opts/osc.conf`

## Lua 脚本

lua 脚本编写, 可参考的资料包括
1. [mpv/lua](https://github.com/mpv-player/mpv/blob/master/DOCS/man/lua.rst#script-location)
2. [manual/lua-scripting](https://mpv.io/manual/master/#lua-scripting)

### Mpv 提供的api

对 Lua 而言, mpv 配置主要提供了 模块 `mp`, 其主要用于发送命令给 `mpv` 内核及得到回馈信息, 下面是其提供的一些方法的主要介绍
- 函数:
    1. 发送命令类:
    ```lua
    command(string), commandv(arg1, arg2, ...), command_native(table, [,def]), command_native_async(table, [,fn])
    ```
