# 远程预设目录

App 的「设置 → 源预设 → 检查源更新」会拉取这里的两份 JSON。App 内置的预设仍然保留，作为离线兜底；远程文件校验不通过时不会覆盖。

## 文件

| 文件 | 内容 | 条数限制 |
|---|---|---|
| `live.json` | 直播源预设目录（分组、名称、地址、镜像、备注） | 5 ~ 300 条 |
| `vod.json` | 点播站点预设（苹果 CMS 采集接口） | 1 ~ 500 条 |

raw 地址（master 分支，路径与文件名保持不变）：

```
https://raw.githubusercontent.com/yitianfadi/livebox-release/master/presets/live.json
https://raw.githubusercontent.com/yitianfadi/livebox-release/master/presets/vod.json
```

## 更新流程

1. 修改对应 JSON；
2. **把 `version` +1**（整数，App 只应用比本地已应用版本更大的清单；忘记加版本号 = 不更新）；
3. 修改 `updatedAt`；
4. 运行 App 仓库里的校验（在 `livebox-x` 目录）：

   ```bash
   node tools/release-presets.mjs --check
   ```

5. push 到 `master`。

需要从 App 的内置预设重新生成初版时（会覆盖对应文件、保留已有 version）：

```bash
node tools/release-presets.mjs --emit
# 同时把 version +1：
node tools/release-presets.mjs --emit --bump
```

## live.json

```json
{
  "version": 1,
  "updatedAt": "2026-10-24 12:00",
  "groups": ["推荐", "综合直播", "TVBox 配置", "IPv6", "广播", "大合集", "其他索引"],
  "sources": [
    {
      "name": "qist 综合直播（tvlive）",
      "url": "https://raw.githubusercontent.com/qist/tvbox/master/tvlive.txt",
      "size": "155KB",
      "group": "推荐",
      "channels": 1420,
      "badge": "",
      "note": "运营商组播较多，公网/无 IPv6 时会有离线，属正常",
      "mirrors": ["https://qist.wyfc.qzz.io/tvlive.txt"]
    }
  ]
}
```

- 远程目录是**整体替换**：App 当前生效的直播预设目录以本文件为准（远程无效/未拉取时用内置）。
- 只影响「添加源 → 预设」列表，不会改动用户已经导入的源。
- 字段与 App 的 `PresetSource` 一一对应，`badge` 是单数。

## vod.json

```json
{
  "version": 1,
  "updatedAt": "2026-10-24 12:00",
  "sites": [
    { "name": "非凡资源", "api": "http://ffzy5.tv/api.php/provide/vod", "filterable": true, "searchable": true }
  ]
}
```

- App 按归一化后的 `api` 合并：本地没有的站点新增；已有站点只同步 `filterable/searchable`（不改名字/api/id）；用户删过的站点（删除墓碑）跳过。
- 从本文件移除某个站点**不会**删除用户已经添加的站点。

## 注意

- 不要在 `update.json` 里混预设版本：那套 `versionCode` 是 App 安装包版本。
- `version` 只用于比较新旧；内容改了就一定要 +1。
