# PRD Generator v4.2 — 生产级产品需求文档生成器

Claude Code / Claude.ai Skill，帮助非技术用户生成可直接交给 AI 开发的完整产品需求文档（PRD）。

## 特性

- 七阶段结构化工作流：需求探查 → 范围裁剪 → 方案设计 → PRD生成 → 扫雷审查 → 上线准备 → 试点迭代
- 139项自动质量检查
- 24项输出质量标准
- 运营者/结果质量/审美三个视角（v4.2）：数据生命周期、AI输出合格标准与数据覆盖、视觉方向确认流程
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
| references/decision-checklist.md | 90项决策确认清单 |
| references/prd-template.md | 28章PRD文档模板 |
| references/security-design.md | 五层安全设计标准 |
| references/resilience-design.md | 容灾/韧性设计标准 |
| references/gap-analysis-checklist.md | 139项扫雷检查 |
| references/go-live-checklist.md | 上线准备检查清单 |
| references/operations-scenarios.md | 运营场景与数据生命周期清单（v4.2） |
| references/ai-quality-and-data-coverage.md | AI输出质量与数据覆盖标准（v4.2） |
| references/data-quality-and-research.md | 用户输入质量与研究/运营指标（v4.2） |
| references/visual-design.md | 视觉设计确认流程（v4.2） |
| references/load-testing.md | 压力测试方法与网络来源（v4.2） |

## 更新记录

### v4.2（2026-11）— 来自一个真实生产系统的试点教训

v4.1 生成的 PRD 在技术层面（并发、安全、容灾）基本可靠，但在一个面向数百名学生的生产系统试点中，暴露出三类工程师视角之外的缺口：

- **运营者视角**：上线一周内补了单个添加、编辑转班、一键解锁、服务端搜索/筛选、重新启用等十余个"老师每天都要用"的功能 → 新增数据生命周期清单
- **结果质量视角**：首批用户 76% 的推荐与专业无关（数据覆盖不足 + 匹配不看专业），另有一批推荐因 AI 输出截断被静默降级 → 新增 AI 合格标准、评测样例集、数据覆盖度矩阵、降级可见
- **审美视角**：功能完整但"不够高级"，因为风格从未与用户对齐 → 新增视觉方向确认流程
- 以及：共用出口 IP 下的限流误伤、真实节奏压测方法、用户敷衍作答的防护与标记、从研究问题反推导出字段、试点迭代闭环

## 许可证

MIT
