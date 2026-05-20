# POE2 Data

POE2 游戏数据更新包 + manifest 托管。

## 结构

```
/
├── manifest.json          # 当前最新版本信息
└── releases/              # GitHub Releases 托管更新包
    └── patch_v{version}.zip
```

## manifest.json

```json
{
  "latest_version": 1,
  "schema_version": 1,
  "compatible_app_versions": ["1.0.0"],
  "download_url": "https://github.com/lovanya/poe2-data/releases/download/v1/patch_v1.zip",
  "package_size": 0,
  "md5": "",
  "changelog": "初始版本"
}
```

### 字段说明

| 字段 | 类型 | 说明 |
|------|------|------|
| `latest_version` | int | 最新数据版本（线性自增） |
| `schema_version` | int | 数据库结构版本 |
| `compatible_app_versions` | string[] | 兼容的 App 版本列表 |
| `download_url` | string | 更新包下载地址（GitHub Releases） |
| `package_size` | int | 包大小（bytes） |
| `md5` | string | 包 MD5 校验 |
| `changelog` | string | 更新说明 |

## 更新包结构

```
patch_v{version}.zip
├── update.sql           # SQL 增量更新
├── poe2.db              # 完整数据库（可选）
├── passives.json        # 天赋树数据
└── media/               # 媒体文件更新
    ├── icons/
    ├── videos/
    └── data/
```

## 发布流程

1. 更新 `manifest.json` 中的 `latest_version`
2. 创建更新包 ZIP
3. 通过 GitHub Releases 发布，tag 为 `v{version}`
4. 更新 `manifest.json` 中的 `download_url` 指向新 Release
