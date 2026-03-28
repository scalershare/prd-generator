# 技术选型决策树

**核心原则：根据项目特征主动推荐最成熟的方案，解释理由。不要给用户一堆选项造成选择困难。用户有异议时再讨论替代方案。**

## 后端语言——顶层决策

```
项目核心特征 → 推荐方案
│
├─ AI密集型（LLM/Embedding/ML） → 推荐 Python(FastAPI)
│  理由：AI生态碾压级优势，所有SDK首先支持Python
│
├─ 超高并发（>1万QPS/百万连接/实时通信） → 推荐 Go(Gin)
│  理由：goroutine天然高并发，内存低，单二进制部署
│
├─ 企业级复杂业务（ERP/CRM/金融/审批流） → 推荐 Java(Spring Boot)
│  理由：企业生态最成熟，工具链最完整
│
├─ 前后端同语言/全栈团队 → 推荐 Node.js/TypeScript(Nest.js)
│  理由：统一语言降低切换成本
│
└─ 无法判断 → 默认推荐 Python(FastAPI)
   理由：学习曲线最低、开发最快、Claude Code生成质量最好
```

### 语言对比表（向用户解释时参考）

| 维度 | Python | Go | Java | Node.js/TS |
|------|--------|-----|------|-----------|
| AI/ML生态 | ★★★★★ | ★★☆ | ★★★ | ★★★ |
| 并发能力 | ★★★(万级) | ★★★★★(百万级) | ★★★★ | ★★★★ |
| 开发速度 | ★★★★★ | ★★★ | ★★★ | ★★★★ |
| Claude Code生成质量 | ★★★★★ | ★★★★ | ★★★★ | ★★★★ |
| 部署体积 | ★★★ | ★★★★★ | ★★ | ★★★ |
| 企业生态 | ★★★★ | ★★★★ | ★★★★★ | ★★★★ |
| 学习曲线 | ★★★★★最低 | ★★★★ | ★★★ | ★★★★ |

### 关键提醒

- <1万QPS的项目，Python/Node.js异步框架就够了，Go的并发优势体现不出来
- AI密集项目选Go/Java，意味着要么桥接Python微服务（架构复杂），要么全用API（费用+延迟增加）
- 小团队短周期项目避免Java（样板代码拖慢速度）
- 尊重用户已有偏好，但必须说明利弊

## 各语言的完整组件推荐

### Python技术栈
```
后端：FastAPI(高性能异步) / Django(全栈+Admin)
ORM：SQLAlchemy 2.0(异步) / Django ORM
数据库：PostgreSQL(默认) / MySQL
缓存：Redis
队列：Celery+Redis / BackgroundTasks(轻量)
前端：Vue 3+Element Plus(国内) / React+Ant Design
状态管理：Pinia(Vue) / Zustand(React)
构建：Vite
部署：Docker+Nginx+Uvicorn
```

### Go技术栈
```
后端：Gin(最流行) / Echo
ORM：GORM / Ent
数据库：PostgreSQL / MySQL
缓存：go-redis
队列：Asynq / goroutine池
前端：Vue 3 / React（前端与后端语言无关）
部署：Docker+单二进制+Nginx
AI：HTTP调API（本地ML需桥接Python服务）
```

### Java技术栈
```
后端：Spring Boot 3.x
ORM：JPA / MyBatis-Plus
数据库：PostgreSQL / MySQL
缓存：Spring Data Redis
队列：Spring Async / RabbitMQ / Kafka
前端：Vue 3 / React
部署：Docker+Jar包+Nginx
注意：JVM内存占用大，小服务器注意分配
```

### Node.js/TypeScript技术栈
```
后端：Nest.js(企业级) / Express(轻量)
ORM：Prisma(推荐) / TypeORM
数据库：PostgreSQL / MySQL / MongoDB
缓存：ioredis
队列：BullMQ+Redis
前端：React+Next.js / Vue 3+Nuxt
部署：Docker+PM2+Nginx
```

## 数据库选择

```
├─ JSON嵌套多/需要向量检索 → PostgreSQL
├─ 简单关系型 → PostgreSQL或MySQL均可
├─ 文档型(Schema灵活) → MongoDB
├─ 亿级分析 → ClickHouse
├─ 用户偏好MySQL → MySQL（提示JSON弱）
└─ 不确定 → 默认PostgreSQL
```

## 常见项目类型的推荐组合

| 项目类型 | 推荐组合 |
|---------|---------|
| AI应用 | Python(FastAPI)+PostgreSQL+Redis+Celery+Vue 3 |
| 企业管理系统 | Java(Spring Boot)+MySQL+Redis+Vue 3 或 Python(Django)+PostgreSQL |
| 高并发API/微服务 | Go(Gin)+PostgreSQL+Redis+gRPC |
| 全栈Web应用 | Node.js(Nest.js)+PostgreSQL+Redis+React(Next.js) |
| 数据分析平台 | Python(FastAPI)+PostgreSQL+Redis+Celery+ECharts |
| 实时通信 | Go(Gin)+PostgreSQL+Redis+WebSocket |
| 小型后台工具 | Python(FastAPI)+SQLite/PostgreSQL+Vue 3 |

## 服务器配置参考

| 用户量 | CPU | 内存 | 磁盘 | 国内月费 | 海外月费 |
|-------|-----|------|------|---------|---------|
| <100 | 2核 | 4G | 40G | ¥100-150 | $15-25 |
| 100-1000 | 4核 | 8G | 100G | ¥200-300 | $40-60 |
| 1000-5000 | 8核 | 16G | 200G | ¥500-800 | $80-120 |
| 5000-1万 | 16核 | 32G | 500G | ¥1500-2500 | $200-350 |
| >1万 | 集群 | 按需 | 按需 | 按需 | 按需 |
