# BLEUnlock

## 请注意：本应用不在 Mac App Store 发布。您可以在这里免费获取！

![CI](https://github.com/ts1/BLEUnlock/workflows/CI/badge.svg)
![Github All Releases](https://img.shields.io/github/downloads/ts1/BLEUnlock/total.svg)
[![Buy me a coffee](img/buymeacoffee.svg)](https://www.buymeacoffee.com/tsone)

BLEUnlock 是一个小巧的菜单栏工具，可以根据 iPhone、Apple Watch 或其他蓝牙低功耗设备的距离自动锁定和解锁您的 Mac。

本文档也提供其他语言版本：[英文](README.md) | [日文](README.ja.md)

## 功能特点

- 无需安装 iPhone 应用
- 可与任何定期发送信号的蓝牙低功耗设备配合使用（需要[静态 MAC 地址](#关于-mac-地址)）
- 当蓝牙设备靠近 Mac 时自动解锁，无需输入密码
- 当蓝牙设备远离 Mac 时自动锁定
- 可选择在锁定/解锁时执行自定义脚本
- 可选择从显示器休眠状态唤醒
- 可选择在离开/返回时暂停/继续播放音乐或视频
- 密码安全存储在钥匙串中
- 可自定义解锁延迟时间（0.5秒至3.0秒，以0.5秒为增量），提供更好的用户体验

## SQHOME-Jin 的修改

此分支版本包含以下增强功能：

1. 添加可自定义解锁延迟时间功能：
   - 默认延迟设置为 0.5 秒
   - 可调范围从 0.5 秒到 3.0 秒
   - 以 0.5 秒为增量进行调整
   - 提供更精确的解锁时间控制

2. 更新界面本地化：
   - 添加"关于"界面的中文本地化
   - 在保留原始版权信息的同时添加修改版本信息
   - 更新主页和版本检查链接指向此分支

3. 改进代码稳定性：
   - 增强解锁延迟菜单处理
   - 修复菜单项状态管理的潜在问题
   - 改进解锁延迟设置的错误处理

## 系统要求

- 支持蓝牙低功耗的 Mac
- macOS 10.13 (High Sierra) 或更高版本
- iPhone 5s 或更新机型、Apple Watch（所有型号），或其他具有[静态 MAC 地址](#关于-mac-地址)且定期发送信号的蓝牙低功耗设备

## 安装方法

### 使用 Homebrew Cask

```
brew install bleunlock
```

### 手动安装

从 [Releases](https://github.com/ts1/BLEUnlock/releases) 下载 zip 文件，解压后将应用移动到应用程序文件夹。

## 设置

首次启动时，需要授予以下权限：

权限 | 说明
-----------|---
蓝牙 | 显然，需要蓝牙访问权限。选择*确定*。
辅助功能 | 解锁锁定屏幕需要此权限。点击*打开系统偏好设置*，点击左下角的锁图标解锁，然后启用 BLEUnlock。
钥匙串 | （不一定会询问）如果询问，必须选择**始终允许**，因为在屏幕锁定时需要此权限。
通知 | （可选）BLEUnlock 在锁定屏幕时会显示消息。这有助于确认其是否正常工作。另外，要在锁定屏幕上看到消息，需要在*通知*偏好设置面板中将*显示预览*设置为*始终*。

> 注意：随着 macOS 版本的更新，所需的权限数量会增加。如果您使用的是旧版本的操作系统，可能不会要求某些权限。

然后，程序会要求输入您的登录密码以解锁屏幕。
密码将安全地存储在钥匙串中。

最后，从菜单栏图标选择*设备*。
它会开始扫描附近的蓝牙低功耗设备。
选择您的设备即可完成设置！

## 选项

选项 | 说明
-------|---
立即锁定屏幕 | 无论蓝牙设备是否在附近都锁定屏幕；当蓝牙设备远离后再次靠近时会解锁。这在离开座位前确保屏幕锁定时很有用。
解锁信号强度 | 解锁所需的蓝牙信号强度。数值越大表示蓝牙设备需要更靠近 Mac 才能解锁。选择*禁用*可禁用解锁功能。
锁定信号强度 | 锁定时的蓝牙信号强度。数值越小表示蓝牙设备需要离 Mac 更远才会锁定。选择*禁用*可禁用锁定功能。
锁定延迟 | 检测到蓝牙设备远离后到锁定 Mac 的时间。如果在此时间内蓝牙设备重新靠近，则不会锁定。
无信号超时 | 最后一次接收到信号到锁定的时间。如果经常出现"信号丢失"锁定，请增加此值。
接近时唤醒 | 当蓝牙设备在锁定状态下接近时，唤醒显示器。
唤醒但不解锁 | 当显示器从休眠状态唤醒时（无论是通过"接近时唤醒"自动唤醒还是手动唤醒），BLEUnlock 不会解锁 Mac。这可以与 macOS 内置的 Apple Watch 解锁功能兼容（可以在 BLEUnlock 唤醒屏幕后立即操作），或者如果您只是希望锁定屏幕更快出现但不想自动解锁。
锁定时暂停"正在播放" | 在锁定/解锁时，BLEUnlock 会暂停/继续播放由*正在播放*小组件或键盘⏯键控制的音乐或视频（包括 Apple Music、QuickTime Player 和 Spotify）。
使用屏幕保护程序锁定 | 如果设置此选项，BLEUnlock 会启动屏幕保护程序而不是锁定。要使此选项正常工作，需要在*安全性与隐私*偏好设置面板中设置*进入睡眠或开始屏幕保护程序**立即**要求输入密码*选项。
锁定时关闭屏幕 | 锁定时立即关闭显示器。
设置密码... | 如果更改了登录密码，请使用此选项。
被动模式 | 默认情况下，它会主动尝试连接蓝牙设备并读取信号强度。大多数情况下，建议使用默认设置，这样最稳定。但是，如果您使用其他蓝牙设备，如键盘、鼠标、触控板，尤其是蓝牙个人热点，默认模式可能会相互干扰。2.4GHz WiFi 也可能造成干扰。如果遇到蓝牙不稳定的情况，请开启被动模式。
登录时启动 | 登录时启动 BLEUnlock。
设置最小信号强度 | 信号强度低于此值的设备不会显示在设备扫描列表中。

## 故障排除

### 在列表中找不到我的设备

如果您的蓝牙设备不是 Apple 设备，BLEUnlock 可能无法找到设备名称。
在这种情况下，您的设备会显示为 UUID（由连字符分隔的长串十六进制数字）。
要识别设备，请尝试将设备靠近或远离 Mac，看信号强度（dB 值）是否相应变化。

如果列表中*完全没有*设备，请尝试按下文所述重置蓝牙模块。

### 无法解锁

确保在*系统偏好设置* > *安全性与隐私* > *隐私* > *辅助功能*中启用了 BLEUnlock。
如果已经启用，请尝试关闭后重新启用。

如果要求访问钥匙串中的密码权限，必须选择*始终允许*，因为在屏幕锁定时需要此权限。

### 经常出现"信号丢失"

增加*无信号超时*值。
或者尝试*被动模式*。

### 我的蓝牙键盘、鼠标、个人热点或其他蓝牙设备出现问题！

首先，按住 Shift + Option 键点击菜单栏或控制中心中的蓝牙图标，然后点击*重置蓝牙模块*。

在 macOS 12 Monterey 中，此选项不再可用。
作为替代，在终端中输入以下命令来重置蓝牙模块：

```
sudo pkill bluetoothd
```

此命令会要求输入登录密码。

如果问题仍然存在，请开启*被动模式*。

## 关于 MAC 地址

与经典蓝牙不同，蓝牙低功耗设备可以使用*私有* MAC 地址。
私有地址可以是随机的，并且可能会随时间变化。

最近的智能设备，无论是 iOS 还是 Android，都倾向于使用每 15 分钟左右就会改变的私有地址。这可能是为了防止跟踪。

另一方面，为了让 BLEUnlock 能够跟踪您的设备，其 MAC 地址必须是静态的。

幸运的是，对于 Apple 设备，如果您使用与 Mac 相同的 Apple ID 登录，MAC 地址会解析为真实（公共）地址。

对于其他设备（包括 Android），目前还不知道如何解析地址。
如果您的非 Apple 设备的 MAC 地址会随时间变化，很遗憾 BLEUnlock 无法支持它。

要检查 MAC 地址是否正确解析，请比较 BLEUnlock 的*设备*扫描列表中显示的 MAC 地址与设备上显示的地址。

## 锁定/解锁时运行脚本

在锁定和解锁时，BLEUnlock 会运行位于以下位置的脚本：

```
~/Library/Application Scripts/jp.sone.BLEUnlock/event
```

根据事件类型传递不同的参数：

|事件|参数|
|-----|--------|
|因信号强度低而被 BLEUnlock 锁定|`away`|
|因无信号而被 BLEUnlock 锁定|`lost`|
|被 BLEUnlock 解锁|`unlocked`|
|手动解锁|`intruded`|

> 注意：要使 `intruded` 事件正常工作，您必须在*安全性与隐私*偏好设置面板中设置*进入睡眠后**立即**要求输入密码*。

### 示例

以下是一个示例脚本，当手动解锁时，它会发送 LINE Notify 消息，并附上 Mac 前方人员的照片。

```sh
#!/bin/bash

set -eo pipefail

LINE_TOKEN=xxxxx

notify() {
    local message=$1
    local image=$2
    if [ "$image" ]; then
        img_arg="-F imageFile=@$image"
    else
        img_arg=""
    fi
    curl -X POST -H "Authorization: Bearer $LINE_TOKEN" -F "message=$message" \
        $img_arg https://notify-api.line.me/api/notify
}

capture() {
    open -Wa SnapshotUnlocker
    ls -t /tmp/unlock-*.jpg | head -1
}

case $1 in
    away)
        notify "$(hostname -s) is locked by BLEUnlock because iPhone is away."
        ;;
    lost)
        notify "$(hostname -s) is locked by BLEUnlock because signal is lost."
        ;;
    unlocked)
        #notify "$(hostname -s) is unlocked by BLEUnlock."
        ;;
    intruded)
        notify "$(hostname -s) is manually unlocked." $(capture)
        ;;
esac
```

`SnapshotUnlocker` 是使用脚本编辑器创建的 .app，其脚本内容如下：

```
do shell script "/usr/local/bin/ffmpeg -f avfoundation -r 30 -i 0 -frames:v 1 -y /tmp/unlock-$(date +%Y%m%d_%H%M%S).jpg"
```

需要此应用是因为 BLEUnlock 没有相机权限。
授予此应用权限可以解决权限问题。

## 致谢

- [peiit](https://github.com/peiit): 中文翻译
- [wenmin-wu](https://github.com/wenmin-wu): 最小信号强度和移动平均
- [stephengroat](https://github.com/stephengroat): CI
- [joeyhoer](https://github.com/joeyhoer): Homebrew Cask
- [Skyearn](https://github.com/Skyearn): Big Sur 风格图标
- [cyberclaus](https://github.com/cyberclaus): 德语、瑞典语、挪威语（书面语）和丹麦语本地化
- [alonewolfx2](https://github.com/alonewolfx2): 土耳其语本地化
- [wernjie](https://github.com/wernjie): 唤醒但不解锁功能
- [tokfrans03](https://github.com/tokfrans03): 语言修正

图标基于从 materialdesignicons.com 下载的 SVG 文件。
这些图标最初由 Google LLC 设计，并根据 Apache License version 2.0 授权。

## 许可证

MIT

Copyright © 2019-2022 Takeshi Sone. 