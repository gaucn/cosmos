# cosmos

MOTE — 单文件 Canvas 交互演示页。

线上地址：**https://cosmos.gaucn.com**

## 部署架构

本仓库通过 GitHub Pages 静态托管，并绑定自定义域名。

```
浏览器访问 cosmos.gaucn.com
        ↓  (CNAME 解析)
<用户名>.github.io
        ↓
本仓库 main 分支根目录的 index.html
```

## 文件说明

| 文件 | 说明 |
|------|------|
| `index.html` | 站点入口（由原始 `mote.html` 重命名，GitHub Pages 要求入口为 `index.html`） |
| `CNAME` | 声明自定义域名 `cosmos.gaucn.com`，删掉它域名就会失效 |
| `.nojekyll` | 跳过 Jekyll 处理，避免以 `_` 或 `.` 开头的文件被忽略 |
| `robots.txt` | 允许搜索引擎抓取 |
| `README.md` | 本说明文件 |

## 自定义域名配置（两处必须一致）

### 1. DNS 解析（域名后台）

| 记录类型 | 主机记录 | 记录值 | TTL |
|----------|----------|--------|-----|
| CNAME | `cosmos` | `<用户名>.github.io` | 600 |

> 子域名用 CNAME，**不要用 A 记录**（A 记录仅用于裸域名如 `gaucn.com`）。
> 记录值填 `<用户名>.github.io`，不是 `<用户名>.github.io/cosmos`。

### 2. GitHub 仓库设置

进入 **Settings → Pages → Custom domain**，填入 `cosmos.gaucn.com` 并 Save。

### 3. 开启 HTTPS

DNS 生效后（通常 10 分钟～24 小时），**Custom domain** 下方会出现
`Enforce HTTPS` 勾选框，务必勾上。GitHub 会自动签发 Let's Encrypt 证书。

> 若勾选框灰色不可选，说明证书还在签发中，等 15～30 分钟刷新页面即可。
> GitHub 签证书前需要 DNS 已正确解析，所以一定要先配好 DNS。

## 常见问题排查

| 现象 | 原因 | 处理 |
|------|------|------|
| 访问显示 404 | `index.html` 不在仓库根目录 | 确认文件位置 |
| 域名解析失败 | CNAME 记录值填错 | 确认是 `<用户名>.github.io` |
| `Enforce HTTPS` 无法勾选 | 证书签发中 / DNS 未生效 | 等待，或先检查 DNS |
| 域名打开显示旧内容 | DNS 缓存 | 清缓存或用无痕模式 |
| 推代码后自定义域名消失 | `CNAME` 文件被删 | 恢复该文件 |

## 本地预览

直接用浏览器打开 `index.html` 即可，无构建步骤、无外部依赖。
