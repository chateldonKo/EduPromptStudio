# 贡献指南

感谢你想要为 EduPrompt Studio 贡献一份力！

本项目最有价值的贡献，**不是写代码**，而是**贡献你单位实际用过的、好用的公文 Prompt 模板**。不需要懂 JavaScript，只需要会写 JSON。

---

## 一、新增一个公文模板（最推荐）

### 1. 在 `data/templates/` 下新建一个 JSON 文件

文件名用英文小写 id，如 `award_evaluation.json`：

```json
{
  "id": "award_evaluation",
  "name": "评奖评优类",
  "icon": "🏅",
  "description": "用于学生综合奖学金、三好学生、优秀干部等评选推荐材料。",
  "structure": [
    "基本情况",
    "主要事迹",
    "推荐理由"
  ],
  "tone": [
    "正式",
    "客观",
    "突出贡献"
  ],
  "forbidden": [
    "无与伦比",
    "全面卓越",
    "绝对第一"
  ],
  "examples": {
    "topic": "国家奖学金推荐材料",
    "background": "申请人为本科三年级学生，专业排名第 1，获国家级竞赛二等奖一项"
  }
}
```

### 2. 在 `data/templates/index.json` 末尾追加 id

```json
{
  "version": 1,
  "templates": [
    "rectification",
    "...",
    "accreditation",
    "award_evaluation"      // ← 新增这一行
  ]
}
```

### 3. 字段规范

| 字段 | 必填 | 说明 |
| --- | :---: | --- |
| `id` | ✅ | 英文小写、用 `_` 分词，与文件名一致 |
| `name` | ✅ | 中文显示名，控制在 8 个字以内 |
| `icon` | ⛔ | 一个 emoji |
| `description` | ✅ | 一句话场景说明（不超过 40 字） |
| `structure` | ✅ | 3–6 项，公文实际的段落结构 |
| `tone` | ✅ | 2–4 个语气词约束 |
| `forbidden` | ✅ | 至少 2 个，这类场景里典型的"AI 套话" |
| `examples` | ⛔ | 真实写过的 `topic` 和 `background`，便于"填入示例数据" |

### 4. 自测

- 在仓库根目录运行 `python -m http.server 8000`
- 访问 <http://localhost:8000>，确认你的模板出现在下拉框，且能生成 Prompt
- 把生成的 Prompt 粘贴到任一大模型，看看输出是否符合预期

### 5. 提交 PR

- 标题：`[Template] 新增「评奖评优类」模板`
- 描述里贴一个用真实场景生成的 Prompt 示例

---

## 二、修复 Bug / 提交新功能

1. Fork 本仓库
2. 新建分支：`git checkout -b fix/short-description`
3. 改动尽量小而聚焦：一次 PR 只解决一件事
4. UI 改动请在移动端宽度（<900px）下也测一遍
5. 提交 PR 并填好模板

---

## 三、代码风格

- 缩进：2 空格
- 字符串：单引号优先（JSON 除外）
- 不引入构建工具：本项目坚持"打开 HTML 就能用"。如果你想引入 React/Vue/打包器，请先在 issue 里讨论
- 不引入运行时依赖：保持纯静态

---

## 四、行为准则

参与本项目即表示你同意遵守 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。

---

## 五、不知道从哪儿下手？

- 找一个 [`good first issue`](https://github.com/chateldonKo/EduPromptStudio/labels/good%20first%20issue) 标签的 issue
- 或者直接发起 Discussion 聊聊你的想法
