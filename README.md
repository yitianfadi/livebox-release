# livebox-release

「直播盒子」App 的发布仓库（源码在 GitHub 私有仓库 `yitianfadi/livebox`）。

- `update.json` —— 应用内「检查更新」读取的版本清单，**路径与文件名永不改**
- **Releases（发行版）** —— 各版本 APK 以发行版附件上传（raw 通道对大文件限登录，放这里才能免登录下载）

## 发版

1. 云打包新 APK（manifest 的 `versionCode` +1、`versionName` 改掉）
2. 创建发行版：tag 用 `v版本号`（如 `v2.0.3`），APK 作为附件上传，命名 `livebox-x.y.z.apk`
3. 改 `update.json`：`versionCode` / `versionName` / `apkUrl`（指向 releases/download 直链）/ `notes` / `pubTime`
4. push
