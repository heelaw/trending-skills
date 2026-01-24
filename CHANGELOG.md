# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-01-24

### 首次发布

**Skills Trending Daily** - 自动追踪 skills.sh 技能排行榜，AI 智能分析，每日趋势报告邮件

### 核心功能

- **Playwright 动态抓取**
  - 使用 Playwright 处理 skills.sh 动态渲染页面
  - 每天自动获取 Top 100 技能排行榜
  - 支持重试机制，提高抓取稳定性
  - 智能解析安装量（支持 "7.0K" 格式）

- **技能详情抓取**
  - 深度抓取热门技能的详细页面
  - 提取完整描述和使用说明
  - 请求间隔控制，避免服务器压力

- **Claude AI 智能分析**
  - 批量总结和分类热门技能
  - 提取摘要、描述、使用场景
  - 智能分类（多种分类支持）
  - 提取解决的问题标签

- **趋势计算引擎**
  - 排名变化计算（上升/下降）
  - 安装量变化率计算
  - 新晋榜单检测
  - 跌出榜单检测
  - 暴涨告警（可配置阈值）

- **SQLite 数据存储**
  - 3 张表：skills_daily、skills_details、skills_history
  - 可配置数据保留天数
  - 支持趋势查询和统计

- **专业 HTML 邮件报告**
  - 无 emoji 设计，专业简洁
  - 每个技能可点击跳转到 skills.sh
  - Top 20 榜单（含 AI 总结）
  - 上升/下降 Top 5
  - 新晋/掉榜展示
  - 暴涨告警高亮

- **Resend 邮件发送**
  - 可靠的邮件发送服务
  - 支持自定义发件人

### 技术栈

- Python 3.11+
- Playwright（浏览器自动化）
- SQLite（数据存储）
- Claude API（AI 分析）
- Resend（邮件服务）

### GitHub Actions

- 每天 UTC 02:00（北京时间 10:00）自动运行
- 支持手动触发
- Playwright 浏览器自动安装
- 数据库自动备份

### 文件结构

```
skills-trending/
├── .github/workflows/
│   └── skills-trending.yml    # GitHub Actions 配置
├── src/
│   ├── config.py              # 配置管理
│   ├── database.py            # SQLite 操作
│   ├── skills_fetcher.py      # 榜单抓取（Playwright）
│   ├── detail_fetcher.py      # 详情抓取
│   ├── claude_summarizer.py   # AI 分析
│   ├── trend_analyzer.py      # 趋势计算
│   ├── html_reporter.py       # 邮件生成
│   ├── resend_sender.py       # 邮件发送
│   └── main_trending.py       # 主入口
├── plugins/
│   └── trending-skills/       # Claude Code Skill
├── requirements.txt
├── .env.example
├── CHANGELOG.md
└── README.md
```

### 环境变量

```bash
# Claude API
ZHIPU_API_KEY=xxx
ANTHROPIC_BASE_URL=https://open.bigmodel.cn/api/anthropic

# Resend 邮件
RESEND_API_KEY=xxx
EMAIL_TO=your@email.com
RESEND_FROM_EMAIL=onboarding@resend.dev

# 数据库
DB_PATH=data/trends.db
DB_RETENTION_DAYS=30

# 告警阈值
SURGE_THRESHOLD=0.3
```

---

[1.0.0]: https://github.com/geekjourneyx/trending-skills/releases/tag/v1.0.0
