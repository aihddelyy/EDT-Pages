# EDT-Pages.github.io

Cloudflare Workers / Pages 反向代理及订阅转换系统的**管理面板前端**，与 [`aihddelyy/edgetunnel`](https://github.com/aihddelyy/edgetunnel) 后端配套使用。

[![GitHub stars](https://img.shields.io/github/stars/EDT-Pages/EDT-Pages.github.io?style=flat-square&logo=github)](https://github.com/EDT-Pages/EDT-Pages.github.io/stargazers)
[![License](https://img.shields.io/github/license/EDT-Pages/EDT-Pages.github.io?style=flat-square)](https://github.com/EDT-Pages/EDT-Pages.github.io/blob/main/LICENSE)

> 🔗 **Demo 演示站点**：[https://EDT-Pages.github.io/admin](https://EDT-Pages.github.io/admin)

---

## 📖 项目简介

EDT-Pages 提供可视化的管理面板，配套 [`edgetunnel`](https://github.com/aihddelyy/edgetunnel) Worker 后端使用。通过静态页面（GitHub Pages 或自建 Pages）托管前端，Worker 通过反向代理的方式让用户在任意域名下都能访问到管理面板。

---

## 🆕 本仓库新增功能（相对上游 `EDT-Pages/EDT-Pages.github.io`）

| 功能 | 说明 |
|------|------|
| 🎯 **个性化 PROXYIP 面板** | 在「反代」模块下新增「启用个性化 PROXYIP」开关与多行编辑器。支持按节点备注中的 `#标签` 分配不同 PROXYIP，单关键词（`#HK`）或多关键词（`#HK\|香港\|HK01`，任一命中即匹配）。 |

---

## 🎯 个性化 PROXYIP 填写说明

### 📝 语法

| 位置 | 分隔符 |
|------|--------|
| **条目之间** | 换行 `\n` 或英文逗号 `,` |
| **同一节点多个关键词** | 仅竖线 `\|`（任一命中即匹配） |

### ✏️ 示例

**单关键词**：
```text
proxyip1.cmliussss.net#HK
proxyip2.cmliussss.net#JP
proxyip3.cmliussss.net:8443#US
[2606:4700::]:2053#IPv6
```

**多关键词（任一命中即匹配）**：
```text
proxyip1.cmliussss.net#HK|香港|HK01
proxyip2.cmliussss.net#JP|东京
proxyip3.cmliussss.net:443#US|洛杉矶
```

**多条目（同一行用逗号拼接）**：
```text
proxyip1.cmliussss.net#HK,proxyip2.cmliussss.net#JP,proxyip3.cmliussss.net#US
```

> [!IMPORTANT]
> - **必须先勾选「启用个性化 PROXYIP」开关**，否则即使填写了内容也不会修改任何节点。
> - **优先级**：与全局 PROXYIP 共存时，节点优先使用个性化 PROXYIP；未匹配到的节点回落到全局 PROXYIP。

---

## ⚙️ 部署

本仓库是**纯静态前端**，通过 GitHub Pages 或 Cloudflare Pages 部署即可。

### 🛠 Pages + GitHub（推荐）

1. Fork 本仓库到你的 GitHub 账户
2. 进入仓库 `Settings` → `Pages`
3. 选择 `Deploy from a branch` → 分支 `main`、目录 `/ (root)` → 保存
4. 等待几分钟后访问 `https://<your-account>.github.io/EDT-Pages.github.io/admin/`

### 🛠 Pages 上传（CF Pages）

1. 将本仓库 `admin/` 目录下的内容打包为 zip
2. 在 Cloudflare 控制台创建 Pages 项目，选择「直接上传」
3. 上传 zip 包即可

### 🔗 关联 Worker

部署好前端后，需在 Worker（[`aihddelyy/edgetunnel`](https://github.com/aihddelyy/edgetunnel)）中配置 `Pages静态页面` 常量指向你的前端地址：

```javascript
const Pages静态页面 = 'https://<your-account>.github.io/EDT-Pages.github.io';
```

---

## 📂 目录结构

```text
EDT-Pages/
├── admin/
│   ├── index.html      # 管理面板主页面（核心文件）
│   └── config.json     # 默认配置示例
├── login/              # 登录页面
├── noADMIN/            # 未配置 ADMIN 时的提示页面
├── noKV/               # 未绑定 KV 时的提示页面
└── README.md           # 本文件
```

---

## 🙏 致谢

- 上游项目：[`EDT-Pages/EDT-Pages.github.io`](https://github.com/EDT-Pages/EDT-Pages.github.io)
- 配套后端：[`cmliu/edgetunnel`](https://github.com/cmliu/edgetunnel)

---

## ⚠️ 免责声明

本项目仅供学习与研究使用，请勿用于任何违法违规用途。使用者应自行承担因使用本项目而产生的一切后果。