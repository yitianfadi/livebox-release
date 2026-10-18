# livebox-release · 直播盒子发布仓库

这个仓库只放**发布物**，不放源码（源码在 GitHub 私有仓库 `yitianfadi/livebox`）。

## 结构

- `update.json` —— App 内「检查更新」读取的版本清单，**文件名和路径永不改**
- `apk/` —— 各版本安装包，文件名带版本号，保留最近几版

## 发版步骤

1. HBuilderX 云打包出新 APK（manifest 的 `versionCode` 必须 +1、`versionName` 改掉）
2. 把 APK 传到 `apk/`，文件名如 `livebox-2.0.3.apk`
3. 修改 `update.json` 的 `versionCode` / `versionName` / `apkUrl` / `notes` / `pubTime`
4. 提交推送，App 端 6 小时内会静默收到提示（或用户手动「检查更新」）

## 地址

- 检查更新：`https://gitee.com/yitianfadi/livebox-release/raw/master/update.json`
