# PRD Generator v4.1 — 生产级产品需求文档生成器

Claude Code / Claude.ai Skill，帮助非技术用户生成可直接交给 AI 开发的完整产品需求文档（PRD）。

## 特性

- 六阶段结构化工作流：需求探查 → 范围裁剪 → 方案设计 → PRD生成 → 扫雷审查 → 上线准备
- 111项自动质量检查
- 19项输出质量标准
- 内置容灾/韧性/安全/兜底设计模板
- 开发陷阱预防（框架兼容性、FK级联、测试隔离、时区统一等）
- 零技术背景用户友好：主动推荐方案，不给用户选择题

## 安装方式

### Claude Code 安装

方法一：使用 Git 克隆到个人 Skills 目录
​```bash
git clone https://github.com/你的用户名/prd-generator.git ~/.claude/skills/prd-generator
​```

方法二：克隆到项目目录（团队共享）
​```bash
git clone https://github.com/你的用户名/prd-generator.git .claude/skills/prd-generator
​```

安装后在 Claude Code 中直接使用，输入相关需求即可自动触发。

### Claude.ai 安装

1. 下载本仓库的 ZIP 文件（Code → Download ZIP）
2. 打开 claude.ai → 设置 → 自定义 → Skills
3. 上传下载的 ZIP 文件

## 文件结构

| 文件 | 用途 |
|------|------|
| SKILL.md | 主入口，工作流定义 |
| references/tech-stack-guide.md | 技术选型决策树 |
| references/decision-checklist.md | 74项决策确认清单 |
| references/prd-template.md | 28章PRD文档模板 |
| references/security-design.md | 五层安全设计标准 |
| references/resilience-design.md | 容灾/韧性设计标准 |
| references/gap-analysis-checklist.md | 111项扫雷检查 |
| references/go-live-checklist.md | 上线准备检查清单 |

## 许可证

MIT
