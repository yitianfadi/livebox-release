# livebox-release

「直播盒子」App 的发布仓库（源码在私有仓库 `yitianfadi/livebox`）。

- `update.json` —— 应用内「检查更新」读取的版本清单，**路径与文件名永不改**
- `presets/live.json` / `presets/vod.json` —— 直播预设目录与点播站点预设；App 设置里手动「检查源更新」拉取，详见 [`presets/README.md`](./presets/README.md)
- **Releases（发行版）** —— 各版本 APK 以发行版附件上传

## 发版

1. 云打包新 APK（manifest 的 `versionCode` +1、`versionName` 改掉）
2. 创建发行版：tag 用版本号（如 `2.0.3`），APK 作为附件上传，命名 `livebox-x.y.z.apk`
3. 改 `update.json`：`versionCode` / `versionName` / `apkUrl`（指向 releases/download 直链）/ `notes` / `pubTime`
4. push

## 地址

- 检查更新：`https://raw.githubusercontent.com/yitianfadi/livebox-release/master/update.json`
- 直播预设：`https://raw.githubusercontent.com/yitianfadi/livebox-release/master/presets/live.json`
- 点播预设：`https://raw.githubusercontent.com/yitianfadi/livebox-release/master/presets/vod.json`
- 附件直链示例：`https://github.com/yitianfadi/livebox-release/releases/download/2.0.3/livebox-2.0.3.apk`
