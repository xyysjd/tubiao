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

在右侧「仓库图标一览」或下方对比列表中：

1. **单个删除**：点图标右上角 **×**
2. **批量删除**：
   - 勾选多个图标（可点卡片空白处切换、全选、反选）
   - 点 **删除选中**
   - 对比区另有 **删除全部**（删掉该侧当前列表里的全部差异项）
3. 规则始终是**只动当前图包**：
   - 删除该图包 `icon/` 下的图片
   - 仅更新该图包 `tubiao.json`
   - 不会修改另一侧
   - 同一图包多个文件只会写一次 JSON

### 图标对比（Fang ↔ Yuan）

页面下方「图标对比」：

1. 配置 Token 后点 **开始对比**
2. 按文件名（不含扩展名，忽略大小写）比较两侧 `icon/` 目录
3. 分别列出 **仅 Fang 有** / **仅 Yuan 有**，并显示共有数量
4. 可用筛选框快速搜名称
5. 支持单个 × / 勾选批量 / 删除全部；完成后自动刷新对比

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
