# Changelog

本项目所有显著的变更都会记录在这个文件里。

格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [Unreleased]

### Added
- 9 类公文模板从 `index.html` 中拆出，迁移到 `data/templates/*.json`
- `data/templates/index.json` 模板清单文件
- 完整 SEO meta：`description` / `keywords` / Open Graph / Twitter Card / canonical / Schema.org JSON-LD
- `favicon.svg`
- 顶部导航：GitHub 链接与「反馈」入口
- 「填入示例数据」按钮，便于新用户快速体验
- AI 生成内容免责声明
- `file://` 协议下的友好错误提示，引导本地用户使用 HTTP 服务器或访问在线版
- 仓库规范化：`.github/ISSUE_TEMPLATE/`（Bug / Feature / Template Request）、`PULL_REQUEST_TEMPLATE.md`、`CONTRIBUTING.md`、`CODE_OF_CONDUCT.md`、`CHANGELOG.md`
- README 重写：价值主张、适用对象对照表、模板字段说明、路线图、FAQ

### Changed
- 移动端表头精简（隐藏次要链接）

## [0.1.0] - 2026-05-14

### Added
- 初版 EduPrompt Studio：单 HTML 文件，9 类高校行政公文模板
- GitHub Pages 部署
