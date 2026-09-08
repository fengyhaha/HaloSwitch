# HaloSwitch

> A fast, visual, window-aware radial switcher for macOS.

[English](#english) · [中文](#中文) · [Download the latest release](../../releases/latest)

<a id="english"></a>

## English

HaloSwitch is a mouse-centred radial switcher built to solve three everyday limitations of the native macOS app switcher:

- **Bring windows back, not just apps.** Native `Command + Tab` can activate a running app without restoring a usable window. HaloSwitch restores hidden or minimized windows and can ask a still-running, windowless app to reopen.
- **Preview before switching.** Hover a window title—or select it with the keyboard—to see a live, low-latency preview at its desktop position.
- **Switch with window-level intent.** HaloSwitch uses a Windows-style window-switching model: it tracks recent switchable windows, validates that they still exist, and returns to the previous usable window rather than treating every app as a single opaque item.

The radial interface still groups windows by app, so you get fast app selection and precise window selection in one workflow.

## Window previews

Enable **Window Previews** to see a window before switching to it:

- Hover a title in the side window menu, or press the backtick key (`` ` ``) to select windows from the keyboard.
- Visible windows refresh at up to approximately 15 FPS after the configured preview delay.
- Minimized windows keep the most recent in-memory frame captured before minimization.
- Choose a longest-edge resolution from 640 px through 2K (2560 px).
- Set the preview delay from immediate to 2 seconds in 100 ms steps.
- Set the in-memory preview cache from 32 MiB to 200 MiB.
- Preview panels fade in and out smoothly and stay below the switcher ring and title menu.

Preview quality depends on what macOS and the target app allow ScreenCaptureKit to capture. Protected video, DRM content, secure system windows, and apps that refuse capture may appear blank or unavailable. A window minimized before HaloSwitch has captured it has no historical frame to display.

## Permissions

HaloSwitch uses two separate macOS permissions:

| Permission | Required? | Used for |
| --- | --- | --- |
| **Accessibility** | **Required** | Intercepting the selected global shortcut; reading, restoring, and raising switchable windows |
| **Screen Recording** | Optional | Capturing window previews only |

App and window switching continues to work if Screen Recording permission is denied or Window Previews is disabled. macOS may display its recording privacy indicator while previews are being captured; that indicator is controlled by the system.

HaloSwitch does not request Screen Recording permission until you explicitly enable Window Previews.

Preview frames stay in memory, are limited by the configured cache size, and are never written to disk or uploaded. HaloSwitch does not record audio.

## Screenshots

<p align="center">
  <img src="screenshots/radial-switcher.png" width="800" alt="HaloSwitch radial switcher">
</p>

<p align="center">
  <img src="screenshots/window-selection.png" width="500" alt="HaloSwitch window selection and preview">
</p>

<p align="center">
  <img src="screenshots/liquid-glass.png" width="400" alt="HaloSwitch Liquid Glass appearance">
  <img src="screenshots/sanded-glass.png" width="400" alt="HaloSwitch classic glass appearance">
</p>

<p align="center">
  <img src="screenshots/settings-english.png" width="400" alt="HaloSwitch Liquid Glass appearance">
  <img src="screenshots/menubar-settings-english.png" width="400" alt="HaloSwitch classic glass appearance">
</p>

## Highlights

### Restore the window you actually want

When available, HaloSwitch starts from the previous recent window that is still running, valid, and raiseable. Closed or stale windows are skipped. Releasing the activation modifier immediately returns to that exact window, while the ring highlights its owning app from the first frame.

Hidden and minimized windows are restored when selected. If an app is still running after its last window was closed, HaloSwitch sends the native macOS reopen request. Apps that have fully quit are not relaunched.

### App ring plus window-level switching

Select an app with `Tab`, `Shift + Tab`, its displayed letter, the scroll wheel, trackpad, or pointer. After the configurable query delay, the side menu shows that app's switchable windows. Press `` ` `` to cycle through them, hover a title to select it, or click a title to open it immediately.

Confirmed attached dialogs and auxiliary windows are treated as part of their host window for focus history. This makes actions such as opening a browser Find dialog and then switching back behave closer to a window-centric Windows switcher.

### Multilingual jump letters

Every app receives a stable jump letter using macOS transliteration, Latin compatibility mappings, and a stable fallback. Choose the full keyboard or left-hand keyboard zone, and optionally hide displayed letters without disabling keyboard jumping.

### Flexible ordering and appearance

Choose recently used, launch order, multilingual alphabetical order, or the current macOS Dock order. Customize the ring radius, icon size, Dock-style magnification, menu typography, scroll sensitivity, classic blur, Liquid Glass, opacity, and scattering radius.

Liquid Glass uses the native macOS appearance on macOS 26 or later. On macOS 15–25, the preference is preserved while HaloSwitch safely renders classic blur.

## Controls

| Action | Result |
| --- | --- |
| `Command + Tab` | Open the ring; configurable as `Option + Tab` or `Control + Tab` |
| Press `Tab` again | Select the next app |
| `Shift + shortcut + Tab` | Select the previous app |
| Press a jump letter | Select the matching app; repeat to cycle matches |
| Scroll down / up | Select clockwise / counterclockwise |
| Hover a ring sector | Select that app |
| Click a ring sector | Open that app immediately |
| Press `` ` `` | Cycle through the selected app's windows and preview the highlighted window |
| Hover a window title | Select and preview that window |
| Click a window title | Open that window immediately |
| Release the activation modifier | Confirm the current selection |
| `Escape` | Cancel switching |

## Installation

1. Download the latest `.dmg` from [Releases](../../releases/latest).
2. Open the DMG and drag **HaloSwitch** into **Applications**.
3. Launch HaloSwitch.
4. Open **System Settings → Privacy & Security → Accessibility** and enable HaloSwitch.
5. Return to the HaloSwitch menu-bar icon and choose **Recheck Accessibility Permission** if interception does not become active immediately.
6. To use previews, enable **Window Previews**, then allow HaloSwitch under **System Settings → Privacy & Security → Screen Recording** (the exact system label may vary by macOS version).

If macOS cannot verify the developer, try opening HaloSwitch once, then go to **System Settings → Privacy & Security** and choose **Open Anyway**.

## Requirements and notes

- macOS 15 or later
- macOS 26 or later for Liquid Glass
- Accessibility permission is required
- Screen Recording permission is required only for optional window previews
- Some third-party apps do not expose or permit access to every window
- All settings and preview data remain local

## Privacy

HaloSwitch requires no account, collects no usage data, and uploads no app names, window titles, keyboard input, or preview images. Accessibility data is used only for switching; preview images remain in the bounded in-memory cache and are discarded automatically.

## License

HaloSwitch is closed-source software. Copying, modification, reverse engineering, redistribution, or commercial use without permission is prohibited.

Copyright © 2026. All rights reserved.

---

<a id="中文"></a>

## 中文

HaloSwitch 是一款以鼠标位置为中心的 macOS 环形切换器，重点解决原生 App 切换器的三个常见痛点：

- **解决原生 `Command + Tab` 无法重新显示窗口的痛点。** App 仍在运行但窗口已经关闭、隐藏或最小化时，原生切换器可能只激活 App，却不显示可用窗口；HaloSwitch 会恢复可恢复的窗口，并可请求仍在运行的无窗口 App 重新打开。
- **鼠标悬浮即可预览窗口内容。** 将指针停留在窗口标题上，或使用键盘选中窗口，即可在桌面原位置查看低延迟预览，确认内容后再切换。
- **采用接近 Windows 的窗口级切换逻辑。** HaloSwitch 以窗口为单位记录最近使用顺序，呼出时检查窗口是否仍然存在且可以置前，优先返回上一个真实可切换的窗口，而不是只把整个 App 当作一个切换单位。

轮盘仍然按 App 对窗口进行分组，因此既保留了 App 级快速选择，也能精确切换到某个窗口。

## 窗口预览

开启 **窗口预览** 后，可以在真正切换前查看目标窗口：

- 鼠标悬停侧边窗口标题，或按反引号键（`` ` ``）使用键盘选择窗口。
- 经过设定的预览延迟后，可见窗口最高以约 15 FPS 更新。
- 窗口最小化后，继续显示最小化前最后一次成功保存在内存中的画面。
- 预览清晰度可从最长边 640 px 调整至 2K（2560 px）。
- 预览延迟可在“立即”至 2 秒之间调节，步进为 100 ms。
- 预览内存缓存可在 32 MiB 至 200 MiB 之间调节。
- 预览窗口带有平滑渐入渐出，并始终位于轮盘和标题菜单下方。

预览效果取决于 macOS 和目标 App 是否允许 ScreenCaptureKit 捕获其内容。受保护视频、DRM 内容、安全系统窗口或拒绝捕获的 App 可能显示空白或“没有可用预览”。如果窗口在 HaloSwitch 第一次捕获前就已经最小化，也无法还原它此前的历史画面。

## 权限说明

HaloSwitch 使用两项相互独立的 macOS 权限：

| 权限 | 是否必需 | 用途 |
| --- | --- | --- |
| **辅助功能** | **必须授权** | 接管设定的全局切换快捷键，以及读取、恢复和置前可切换窗口 |
| **屏幕录制** | 仅预览需要 | 捕获窗口预览画面，不用于 App 或窗口切换本身 |

拒绝屏幕录制权限或关闭窗口预览，不会影响 HaloSwitch 的 App 和窗口切换功能。捕获预览期间，macOS 可能显示系统录屏隐私指示图标；该图标由系统控制。

在你主动开启窗口预览之前，HaloSwitch 不会申请屏幕录制权限。

预览画面只保存在受容量限制的内存缓存中，不会写入磁盘或上传网络。HaloSwitch 不会录制音频。

## 界面预览

<p align="center">
  <img src="screenshots/radial-switcher.png" width="800" alt="HaloSwitch 环形轮盘">
</p>

<p align="center">
  <img src="screenshots/window-selection.png" width="500" alt="HaloSwitch 窗口选择和预览">
</p>

<p align="center">
  <img src="screenshots/liquid-glass.png" width="400" alt="HaloSwitch 液态玻璃界面">
  <img src="screenshots/sanded-glass.png" width="400" alt="HaloSwitch 经典毛玻璃界面">
</p>

<p align="center">
  <img src="screenshots/settings-chinese.png" width="400" alt="HaloSwitch Liquid Glass appearance">
  <img src="screenshots/menubar-settings-chinese.png" width="400" alt="HaloSwitch classic glass appearance">
</p>

## 主要特点

### 返回真正需要的窗口

有可用窗口历史时，HaloSwitch 会从最近使用的窗口开始，依次检查目标 App 是否仍在运行、窗口是否仍然有效并支持置前。已经关闭或失效的窗口会被跳过。轮盘第一次出现时就会选中最终目标窗口所属的 App；直接松开修饰键，则返回同一个窗口。

选择隐藏或最小化窗口时，HaloSwitch 会将其恢复。如果 App 进程仍在运行，但最后一个窗口已经关闭，HaloSwitch 会发送 macOS 原生重新打开请求；已经完全退出的 App 不会被重新启动。

### App 轮盘与窗口级切换结合

你可以使用 `Tab`、`Shift + Tab`、跳转字母、滚轮、触控板或鼠标选择 App。经过可调节的窗口查询延迟后，侧边菜单会显示该 App 中真实可切换的窗口。按 `` ` `` 可循环选中窗口，悬停标题可选择窗口，点击标题则立即打开。

能够被系统关系明确确认的对话框和辅助窗口会在焦点历史中归入其宿主窗口。因此，在浏览器中打开页面搜索框后再切换时，行为会更接近以窗口为单位管理的 Windows 切换器。

### 多语言跳转字母

HaloSwitch 通过 macOS 系统转写、拉丁兼容映射和稳定回退，为每个 App 分配可用字母。你可以选择全键盘或左手键盘区方案，也可以隐藏轮盘上的字母而不关闭键盘跳转。

### 灵活的排序与外观

App 可按最近使用、打开顺序、多语言首字母或当前 Dock 顺序排列。你还可以调整轮盘半径、图标大小、Dock 风格放大倍率、菜单文字、滚动灵敏度、经典毛玻璃、液态玻璃、不透明度和散射半径。

液态玻璃在 macOS 26 或更高版本中使用系统原生效果；macOS 15–25 会保存该选择，并安全回退为经典毛玻璃。

## 操作指南

| 操作 | 效果 |
| --- | --- |
| `Command + Tab` | 呼出轮盘；可改为 `Option + Tab` 或 `Control + Tab` |
| 继续按 `Tab` | 选择下一个 App |
| `Shift + 快捷键 + Tab` | 选择上一个 App |
| 按跳转字母 | 选择匹配的 App；重复按键可循环选择 |
| 滚轮或触控板向下／向上 | 顺时针／逆时针选择 App |
| 悬停轮盘扇形 | 选中对应 App |
| 点击轮盘扇形 | 立即打开对应 App |
| 按反引号键 `` ` `` | 循环选择当前 App 的窗口，并预览高亮窗口 |
| 悬停窗口标题 | 选择并预览该窗口 |
| 点击窗口标题 | 立即打开该窗口 |
| 松开呼出快捷键的修饰键 | 确认当前选择 |
| `Escape` | 取消本次切换 |

## 安装方法

1. 在 [Releases](../../releases/latest) 下载最新的 `.dmg` 文件。
2. 打开 DMG，将 **HaloSwitch** 拖入 **Applications（应用程序）** 文件夹。
3. 启动 HaloSwitch。
4. 前往 **系统设置 → 隐私与安全性 → 辅助功能**，开启 HaloSwitch。
5. 如果快捷键没有立即被接管，请返回 HaloSwitch 菜单栏图标并选择 **重新检查辅助功能权限**。
6. 如需窗口预览，请在设置中开启 **窗口预览**，然后前往 **系统设置 → 隐私与安全性 → 屏幕录制（或“屏幕与系统音频录制”）** 授权 HaloSwitch。

如果 macOS 提示无法验证开发者，请先尝试打开 HaloSwitch 一次，然后前往 **系统设置 → 隐私与安全性**，找到 HaloSwitch 并选择 **仍要打开**。

## 系统要求与使用说明

- macOS 15 或更高版本
- 液态玻璃需要 macOS 26 或更高版本
- 必须授予辅助功能权限
- 只有启用可选的窗口预览时才需要屏幕录制权限
- 某些第三方 App 不会公开或允许捕获全部窗口
- 所有设置和预览数据均保存在本机

## 隐私说明

HaloSwitch 不需要账号，不收集使用数据，也不会上传 App 名称、窗口标题、按键内容或预览图片。辅助功能数据仅用于窗口切换；预览画面只存在于容量受限的内存缓存中，并会自动释放。

## 支持 HaloSwitch

如果 HaloSwitch 对你有所帮助，并且你愿意支持后续开发，可以通过微信或支付宝请我喝杯咖啡 ☕️。

<table>
  <tr>
    <td align="center">
      <img src="support/wechat.jpg" width="220" alt="微信收款码"><br>
      <strong>微信支付</strong>
    </td>
    <td align="center">
      <img src="support/alipay.jpg" width="220" alt="支付宝收款码"><br>
      <strong>支付宝</strong>
    </td>
  </tr>
</table>

感谢你对 HaloSwitch 的支持 ❤️

## 软件许可

HaloSwitch 为闭源软件。未经许可，不得复制、修改、反编译、重新分发或用于商业用途。

Copyright © 2026. All rights reserved.
