# PowerKeyCamera（雙擊電源鍵快啟相機）

[![Release](https://img.shields.io/github/v/release/dx9901mk5/PowerKeyCamera)](https://github.com/dx9901mk5/PowerKeyCamera/releases)
[![Android](https://img.shields.io/badge/Android-8.0%2B-3DDC84)](https://developer.android.com)
[![Shizuku](https://img.shields.io/badge/Powered%20by-Shizuku-4285F4)](https://shizuku.rikka.app/)

[繁體中文](#繁體中文說明) | [English](#english)

---

<a id="繁體中文說明"></a>
## 繁體中文說明

透過 **Shizuku**（`uid=2000` / `shell` 權限）監聽底層電源鍵連擊事件，在 **vivo OriginOS / Android** 上實現「雙擊電源鍵快速啟動相機」。

### 主要特色
- **鎖屏 / 黑屏安全相機直呼**：支援以 `VIVO_STILL_IMAGE_CAMERA_SECURE`（或標準 `STILL_IMAGE_CAMERA_SECURE`）直接覆蓋鎖屏介面啟動相機，無需解鎖即可拍照（僅可瀏覽剛拍下的照片，無法檢視舊相簿）。
- **三級自動備援按鍵注入**：支援模擬連按兩下音量下鍵通道（Tier 1 `/dev/input/eventX` → Tier 2 `InputManager` 反射注入 → Tier 3 `input keyevent 25` 錯開執行），可於 App 內一鍵測試並即時顯示實際使用的注入通道。
- **智慧狀態分流**：已解鎖亮屏時自動改以 `STILL_IMAGE_CAMERA` 啟動相機，避免看影片或聽音樂時誤觸調降音量。
- **觸發條件三選一**：
  1. 不管螢幕解鎖還是不解鎖都可以觸發（預設）
  2. 僅螢幕上鎖（含黑屏）才觸發
  3. 僅螢幕解鎖才觸發
- **開機自動啟動與守護進程**：透過 Shizuku `UserService (daemon=true)` 常駐監聽，支援開機／更新後自動啟動，並於啟動時自動清理舊版殘留守護進程。
- **內建雲端更新檢查**：支援正式版／測試版頻道切換，偵測到新版 APK 後可自動下載並喚起系統安裝。
- **Material 3 Dark 自適應介面**：支援深藍科技／橘暗雙主題切換、Edge-to-Edge 與摺疊屏／平板雙欄自適應排版。

### 使用需求與設定
1. Android 8.0+（建議 vivo OriginOS 裝置，亦可於其他 Android 裝置使用安全相機／音量鍵通道）。
2. 已安裝並啟動 **[Shizuku](https://shizuku.rikka.app/)**，並授權本應用使用 Shizuku。
3. 若選擇「模擬雙擊音量下鍵」模式，請在 OriginOS 系統設定中開啟：**設定 > 快捷與輔助 > 快捷啟動 > 連按兩下音量下鍵啟動相機**。

### 下載安裝
請前往 [Releases](https://github.com/dx9901mk5/PowerKeyCamera/releases) 下載最新 APK 安裝。

---

<a id="english"></a>
## English

**PowerKeyCamera** is a lightweight Android utility powered by **Shizuku** (`uid=2000` / `shell` privilege) that monitors low-level hardware power-button double-press events to launch the camera quickly on **vivo OriginOS / Android** devices.

### Key Features
- **Direct Secure Camera on Lockscreen / Screen-Off**: Supports launching `VIVO_STILL_IMAGE_CAMERA_SECURE` (with fallback to `STILL_IMAGE_CAMERA_SECURE`) + `KEYCODE_WAKEUP` directly over the lockscreen—allowing instant photo capture without unlocking while keeping existing gallery photos protected.
- **3-Tier Key Injection Fallback**: Supports double volume-down simulation (`KEYCODE_VOLUME_DOWN`) with automatic fallback (`Tier 1: /dev/input/eventX` → `Tier 2: InputManager reflection` → `Tier 3: staggered input keyevent 25`), plus a built-in diagnostic test card.
- **Smart Unlock Routing**: Automatically launches standard `STILL_IMAGE_CAMERA` when the device is already unlocked, preventing accidental volume drops during media playback.
- **Flexible Trigger Scope**:
  1. Trigger regardless of lock state (Default)
  2. Trigger only when locked or screen-off
  3. Trigger only when unlocked
- **Boot Auto-Start & Daemon Hygiene**: Runs as a persistent Shizuku `UserService (daemon=true)`, supports auto-starting after device boot or app update, and automatically cleans up stale daemon processes.
- **In-App Auto-Updater**: Supports Release and Test channels with automatic APK download and installer launch.
- **Material 3 Adaptive Dark UI**: Features dual dark themes (Deep Blue / Orange Dark), Edge-to-Edge insets, and responsive two-column layout for foldables and tablets (`>= 600dp`).

### Requirements
1. Android 8.0+ (optimized for vivo OriginOS; works on standard Android devices as well).
2. **[Shizuku](https://shizuku.rikka.app/)** running and authorized for PowerKeyCamera.
3. If using the "Simulate Double Volume Down" mode on OriginOS, enable the system setting: **Settings > Shortcuts & Accessibility > Quick Action > Press Volume Down twice to open Camera**.

### Download
Download the latest APK from [Releases](https://github.com/dx9901mk5/PowerKeyCamera/releases).
