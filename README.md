# xsytem35-sdl2

这是 `xsystem35` 的多平台移植版本，`xsystem35` 是 AliceSoft 的 System 3.x 游戏引擎的一个自由实现。

## 兼容性

请参阅[游戏兼容性列表](https://game_compatibility.md/)，了解可以使用 xsystem35-sdl2 运行的游戏列表。

## 独特功能

除了原始 System 3.x 的功能之外，xsystem35-sdl2 还提供了以下特性：

### 播放音频文件作为虚拟 CD 音乐

许多 System 3.x 游戏将音乐以 CD-ROM 上的音轨形式提供。xsystem35 可以从音频文件播放音乐，无需插入 CD。支持的音频文件格式为 MP3 和 Ogg。要使用抓取的音频文件，请在游戏目录中创建一个名为 `playlist.txt` 的文件，并逐行列出声轨文件的路径。例如：

text

```
# 第一行不使用
BGM/track02.mp3
BGM/track03.mp3
...
```



第一行不使用，因为游戏 CD 上的第一轨通常是数据轨。

有些游戏将音乐集成为了 MIDI。在这种情况下，虚拟 CD 功能无法播放音乐。如果你遇到 `Cannot load MIDI` 错误信息，可能需要设置 `SDL_SOUNDFONTS` 环境变量，使其指向一个 `.sf2` 文件。例如：

text

```
SDL_SOUNDFONTS=/usr/share/soundfonts/GeneralUser.sf2 xsystem35
```



### Unicode 翻译支持

原始 System 3.x 仅支持 Shift_JIS（一种日文字符编码），而 xsystem35 支持 Unicode，并且可以运行翻译成日语和英语之外其他语言的游戏。

有关如何构建支持 Unicode 的游戏，请参阅 [xsys35c](https://github.com/kichikuou/xsys35c) 文档。

### 调试

xsystem35 内置了一个调试器，允许你单步执行游戏，并检查或修改游戏变量。有两种使用调试器的方式：

- 通过 [Visual Studio Code](https://code.visualstudio.com/)（推荐）：[vscode-system3x](https://github.com/kichikuou/vscode-system3x) 扩展为 System 3.x 提供了图形化调试界面。
- 使用命令行调试器：使用 `-debug` 选项运行 xsystem35 将启动带有控制台界面的调试器。输入 `help` 查看可用命令列表。

### 直播模式

xsystem35 引入了“直播模式”，使含有 NSFW 内容的游戏在直播或公开观看时更加安全。当使用 `-censor <文件>` 选项启用该模式后，指定文件中列出的图像会被自动打上马赛克。

`misc/censor/` 目录包含了一些游戏的示例审查列表文件。

## 安装

预构建的 Windows 和 Android 安装包可以从 [Releases](https://github.com/kichikuou/xsystem35-sdl2/releases) 页面下载。

Windows 注意事项：

- 64 位版本支持 Windows 10 或更高版本。对于旧版 Windows，请使用 32 位版本。
- 调试功能仅在 64 位版本中支持。

对于其他平台，请参考构建部分。

## 运行

### Windows

将 `xsystem35.exe` 复制到游戏文件夹中，然后运行它。

### Android

请参阅 [android/README.md](https://android/README.md#usage)。

### 其他平台

在游戏目录内运行 xsystem35。

bash

```
$ cd /path/to/game_directory
$ xsystem35
```



详细用法请参阅 [xsystem35 命令手册](https://doc/xsystem35.6.adoc)。

## 构建

### Linux（Debian / Ubuntu）

bash

```
$ sudo apt install build-essential cmake libgtk-3-dev libsdl2-dev libsdl2-ttf-dev libsdl2-mixer-dev libwebp-dev libportmidi-dev libcjson-dev asciidoctor
$ mkdir -p out/debug
$ cd out/debug
$ cmake -DCMAKE_BUILD_TYPE=Debug ../../
$ make && make install
```



### macOS

需要安装 [Homebrew](https://brew.sh/)。

bash

```
$ brew install cmake pkg-config sdl2 sdl2_mixer sdl2_ttf webp portmidi cjson asciidoctor
$ mkdir -p out/debug
$ cd out/debug
$ cmake -DCMAKE_BUILD_TYPE=Debug ../../
$ make && make install
```



### Windows

需要安装 [MSYS2](https://www.msys2.org/)。

bash

```
$ pacman -S cmake mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-cmake mingw-w64-ucrt-x86_64-SDL2 mingw-w64-ucrt-x86_64-SDL2_ttf mingw-w64-ucrt-x86_64-SDL2_mixer mingw-w64-ucrt-x86_64-libwebp mingw-w64-ucrt-x86_64-portmidi mingw-w64-ucrt-x86_64-cjson
$ mkdir -p out/debug
$ cd out/debug
$ cmake -G"MSYS Makefiles" -DCMAKE_BUILD_TYPE=Debug ../../
$ make
```



### Emscripten

bash

```
$ mkdir -p out/wasm
$ cd out/wasm
$ emcmake cmake -DCMAKE_BUILD_TYPE=MinSizeRel ../../
$ make
```



要使用生成的二进制文件，请查看 [Kichikuou on Web](https://github.com/kichikuou/web)，并将 `out/xsystem35.*` 复制到其 `docs` 目录中。

### Android

请参阅 [android/README.md](https://android/README.md)。