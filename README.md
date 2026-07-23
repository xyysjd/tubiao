# tubiao · Emby / Fileball 图标包

自用图标仓库，包含 **方（Fang）** 与 **圆（Yuan）** 两套图标，并附带 GitHub Pages 管理站：上传图片后自动写入 `icon/` 目录、更新对应 `tubiao.json`。

## 图标包地址（给 Fileball 用）

| 图包 | JSON 地址 |
|------|-----------|
| 方 Fang | `https://raw.githubusercontent.com/xyysjd/tubiao/main/Fang/tubiao.json` |
| 圆 Yuan | `https://raw.githubusercontent.com/xyysjd/tubiao/main/Yuan/tubiao.json` |

## 管理站（上传新图标）

启用 GitHub Pages 后访问：

**https://xyysjd.github.io/tubiao/**

### 第一次使用

1. 打开仓库 **Settings → Pages**
   - Source：`Deploy from a branch`
   - Branch：`main` / `/ (root)`
   - 保存后稍等 1–2 分钟
2. 创建 [Fine-grained Personal Access Token](https://github.com/settings/tokens?type=beta)
   - Resource owner：你的账号
   - Repository access：只选 `tubiao`
   - Permissions → Repository permissions → **Contents: Read and write**
3. 打开管理站，粘贴 Token 点「保存」，再点「测试连接」
4. 拖入 PNG（可多选），选择 Fang / Yuan / 两者，确认「JSON 显示名」和「文件名」，点「上传并更新 JSON」

Token 只存在浏览器 `localStorage`，不会发到第三方；建议仅在本机使用。

### 上传时会发生什么

对每个选中的图包：

1. 图片写入 `{Fang|Yuan}/icon/{文件名}.png`
2. 在 `{Fang|Yuan}/tubiao.json` 中按名称插入/更新条目：
   ```json
   {
     "name": "显示名",
     "url": "https://raw.githubusercontent.com/xyysjd/tubiao/main/Fang/icon/显示名.png"
   }
   ```
3. 通过 GitHub API 直接提交到 `main` 分支

### 删除图标

在右侧「仓库图标一览」中：

1. 选择 Fang / Yuan，可搜索名称
2. 鼠标悬停图标，点右上角 **×**
3. 确认后会：
   - 删除 `icon/` 下的图片文件
   - **扫描 Fang + Yuan 两个** `tubiao.json`，移除所有 `url` 指向该图片的条目  
     （含跨包引用，例如 Fang 的 JSON 指向 Yuan 图片）
   - 直接提交到 `main`

### 本地开发

仓库本身是静态文件，本地打开 `index.html` 也能用（仍走 GitHub API）。

```bash
# 可选：本地静态预览
npx --yes serve .
```

## 目录结构

```
tubiao/
├── index.html          # 管理站
├── README.md
├── Fang/
│   ├── icon/           # 方图标 PNG
│   └── tubiao.json
└── Yuan/
    ├── icon/           # 圆图标 PNG
    └── tubiao.json
```

## 说明

- 图标命名建议用服名/群名，方便 Fileball 搜索。
- JSON 中仍包含上游 [Softlyx/Fileball](https://github.com/Softlyx/Fileball) 的引用；本仓库新增图标指向 `xyysjd/tubiao`。
- 若管理站提示 SHA 冲突，刷新后重试（有人同时改了同一文件）。
