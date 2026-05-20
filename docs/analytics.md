# 隐私友好的访问统计接入指南

你需要知道**哪些模板最热门、用户从哪儿来、哪些功能被点了**——但不想用 Google Analytics 那种"全员卖数据"的方案。

下面三个方案任选其一，都满足：

- 不放任何第三方 cookie
- 不需要 GDPR / Cookie 同意条
- 站点速度不受影响（脚本 < 2KB）
- 中国大陆地区访问无障碍（Plausible 国际版除外，已标注）

`index.html` 已经在 `<head>` 里预留了注释占位，启用时只需要取消注释并替换 `data-website-id`。

## 方案对比

| 维度 | Umami（自部署） | Plausible Cloud | GoatCounter |
| --- | --- | --- | --- |
| 价格 | 免费（自部署）| 9 美元/月起 | 个人版免费 |
| 国内访问 | ✅ 取决于你部署的服务器 | ⚠️ 国际线路偶尔慢 | ✅ 稳定 |
| 数据归属 | 100% 自己的服务器 | Plausible 服务器 | GoatCounter 服务器 |
| 部署难度 | 中（需要一台 VPS） | 零部署 | 零部署 |
| 适合谁 | 想完全掌控数据 | 想最省事 | 个人小流量场景 |

**个人副业项目推荐顺序：GoatCounter → Umami → Plausible**。先用 GoatCounter 跑起来，等月访问超 5k 再考虑迁移。

---

## 方案 A：GoatCounter（最简单）

### 1. 注册

打开 <https://www.goatcounter.com/signup>，创建一个免费账户，选一个二级域名（如 `eduprompt.goatcounter.com`）。

### 2. 在 index.html 启用

打开项目根目录的 `index.html`，找到注释块：

```html
<!--
  📈 隐私友好的访问统计（可选）。
  ...
-->
```

把它替换为：

```html
<script data-goatcounter="https://eduprompt.goatcounter.com/count"
        async src="//gc.zgo.at/count.js"></script>
```

提交 → push → GitHub Pages 自动更新，几分钟内就能在 GoatCounter 后台看到访问数据。

### 3. （可选）记录关键事件

在生成 Prompt 后追加一行：

```js
if (window.goatcounter) {
  goatcounter.count({
    path: 'generate/' + id,   // 例如 generate/rectification
    event: true
  });
}
```

这样后台就能看到"哪个模板被点了多少次"。

---

## 方案 B：Umami（自部署，推荐进阶玩家）

### 1. 部署

最快的方式是 Railway 一键模板或 Vercel + Supabase Postgres：

```bash
git clone https://github.com/umami-software/umami.git
cd umami
# 见 https://umami.is/docs/install 选择你熟悉的部署方式
```

部署完成后访问 Umami 后台，新增一个站点 `chateldonko.github.io/EduPromptStudio`，复制 `data-website-id`。

### 2. 在 index.html 启用

```html
<script defer src="https://你的umami地址/script.js"
        data-website-id="刚才复制的-website-id"></script>
```

### 3. （可选）事件追踪

```js
if (window.umami) umami.track('generate-prompt', { template: id });
```

---

## 方案 C：Plausible

### 1. 注册

<https://plausible.io/>，9 美元/月起。如果你在意国内访问速度，可以选 `plausible.io/zh` 自部署，过程类似 Umami。

### 2. 启用

```html
<script defer data-domain="chateldonko.github.io"
        src="https://plausible.io/js/script.js"></script>
```

---

## 你最应该看的 3 个指标

不管选哪个方案，每周看一次以下三个数字就够了：

1. **唯一访客数**：是否在增长？哪天有突增？复盘当天发了什么内容
2. **TOP 5 模板**：哪些模板最被使用？这是你下一步迭代的重点方向
3. **来源 / Referrer**：从哪些渠道进来？小红书、公众号、知乎、自然搜索的比例

> 别看跳出率。纯前端工具站点跳出率天然就高（用户复制 Prompt 就走了），没参考意义。

---

## 一行隐私声明

启用任意统计后，建议在 README 的 FAQ 加一句：

> **Q：会上传我的数据吗？**
> A：本工具的所有 Prompt 输入仅在浏览器本地处理，不发往任何服务器。站点会用 \[GoatCounter / Umami / Plausible\] 收集匿名访问统计（页面访问、Referrer、屏幕尺寸），不收集 IP 明文、不放第三方 cookie、不能追踪个人。
