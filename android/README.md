# xsystem35 for Android

最低支持的 Android 版本：5.0

## 下载

你可以从以下地址下载预编译的 APK：
https://github.com/kichikuou/xsystem35-sdl2/releases

### 使用 Obtainium 安装

另外，你也可以通过 [Obtainium](https://github.com/ImranR98/Obtainium) 安装 `xsystem35-sdl2`。Obtainium 会自动检测新版本并允许你直接更新应用。

1. 在你的 Android 设备上安装 Obtainium。

2. 点击下面的徽章，将应用添加到 Obtainium 中：

   [](https://apps.obtainium.imranr.dev/redirect?r=obtainium://app/%7B%22id%22%3A%22io.github.kichikuou.xsystem35%22%2C%22url%22%3A%22https%3A%2F%2Fgithub.com%2Fkichikuou%2Fxsystem35-sdl2%22%2C%22author%22%3A%22kichikuou%22%2C%22name%22%3A%22xsystem35%22%2C%22categories%22%3A%5B%22games%22%5D%7D)

## 使用方法

### 基本操作

1. 创建一个包含所有游戏文件和 BGM 文件的 ZIP 压缩包（详情请见下文），并将其传输到你的设备上。
2. 打开应用。点击右上角的选项菜单（三个点），选择“Install from ZIP”（从 ZIP 安装）。
3. 选择你在第 1 步中创建的 ZIP 文件。
4. 游戏将启动。要模拟右键点击，请点击屏幕左侧或右侧、上方或下方的黑边区域。

### 准备 ZIP 文件

- 包含 `GAMEDATA` 文件夹中的所有文件（例如 `.ALD` 文件等）。`.EXE` 和 `.DLL` 文件不是必需的，但如果你愿意也可以包含。
- 音乐文件（`.mp3`、`.ogg` 或 `.wav`），如果文件名开头或扩展名之前有数字，则会被识别为 BGM 文件。例如：
  - `Track2.mp3`
  - `15.ogg`
  - `02 - Title.mp3`
  - `rance4_03.wav` （注意：文件名不应为 `rance403.wav`，否则会被当作第 403 首曲目）

注意：此 ZIP 格式也与 [Kichikuou on Web](http://kichikuou.github.io/web/) 兼容。

### 其他功能

- 你可以通过游戏列表的选项菜单导出或导入存档文件。
- 要卸载游戏，请在游戏列表中长按其标题。

## 已知问题

- Android 7.0 以下的版本无法处理包含 Shift-JIS 文件名的 ZIP 文件。此问题出现在 [retroc.net](http://retropc.net/alice/) 上分发的一些 ZIP 文件中。如果你遇到“This type of ZIP is not supported”（不支持此类型的 ZIP）的错误信息，请在电脑上解压该文件，并使用现代的 ZIP 压缩软件重新打包。

## 从源代码构建

### 使用 Android Studio

将本目录作为 Android Studio 项目打开。

### 命令行构建

设置环境变量，然后在本目录中运行 `gradlew` 脚本。

构建示例（适用于 Debian bookworm）：

sh

```
# 安装必要的软件包
sudo apt install git wget unzip default-jdk-headless ninja-build

# 安装 Android SDK / NDK
export ANDROID_SDK_ROOT=$HOME/android-sdk
mkdir -p $ANDROID_SDK_ROOT/cmdline-tools
wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
unzip commandlinetools-linux-11076708_latest.zip -d $ANDROID_SDK_ROOT/cmdline-tools
mv $ANDROID_SDK_ROOT/cmdline-tools/cmdline-tools $ANDROID_SDK_ROOT/cmdline-tools/tools
yes | $ANDROID_SDK_ROOT/cmdline-tools/tools/bin/sdkmanager --licenses
$ANDROID_SDK_ROOT/cmdline-tools/tools/bin/sdkmanager ndk-bundle 'cmake;3.22.1'
export ANDROID_NDK_HOME=$ANDROID_SDK_ROOT/ndk-bundle

# 克隆并构建 xsystem35
git clone https://github.com/kichikuou/xsystem35-sdl2.git
cd xsystem35-sdl2/android
./gradlew build  # 如果你有连接的设备，也可以运行 ./gradlew installDebug
```
