# livebox-release

「直播盒子」App 的发布仓库（源码在 GitHub 私有仓库 `yitianfadi/livebox`）。

- `update.json` —— 应用内「检查更新」读取的版本清单，**路径与文件名永不改**
- `apk/` —— 各版本安装包，文件名带版本号

## 发版

1. 云打包新 APK（manifest 的 `versionCode` +1、`versionName` 改掉）
2. APK 传到 `apk/`，命名 `livebox-x.y.z.apk`
3. 改 `update.json`：`versionCode` / `versionName` / `apkUrl` / `notes` / `pubTime`
4. push
