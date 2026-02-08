# 🚀 Skills Trending 部署指南

## ✅ 已完成的步骤

- ✅ 创建 GitHub 仓库: `https://github.com/heelaw/trending-skills`
- ✅ 推送代码到仓库
- ✅ GitHub Actions 工作流已配置

## 📝 需要你完成的配置

### 步骤 1: 配置 GitHub Secrets

访问: `https://github.com/heelaw/trending-skills/settings/secrets/actions`

点击 "New repository secret" 添加以下 Secrets:

| Secret 名称 | 值 | 说明 |
|------------|-----|------|
| `ZHIPU_API_KEY` | `ACNLFIBFLBMEGBEL` | 智谱 AI API Key (已提供) |
| `RESEND_API_KEY` | 你的 Resend API Key | 邮件服务 API Key |
| `EMAIL_TO` | 你的邮箱地址 | 接收报告的邮箱 |

### 步骤 2: 获取 Resend API Key (可选)

如果你想使用邮件通知功能:

1. 访问 [resend.com](https://resend.com)
2. 注册账号并获取 API Key
3. 将 API Key 添加到 GitHub Secrets

**或者使用免费邮件方式:**
- 修改 `.github/workflows/skills-trending.yml`
- 注释掉 Resend 部分，使用 SMTP

### 步骤 3: 测试 GitHub Actions

1. 访问: `https://github.com/heelaw/trending-skills/actions`
2. 点击 "Skills trending" 工作流
3. 点击 "Run workflow" 手动触发测试

### 步骤 4: 查看结果

运行成功后，查看:
- **Actions 日志**: https://github.com/heelaw/trending-skills/actions
- **代码提交历史**: https://github.com/heelaw/trending-skills/commits/master

## ⏰ 自动运行时间

工作流会在每天 **UTC 02:00** (北京时间 **10:00**) 自动运行

## 🛠️ 自定义配置

### 修改运行时间

编辑 `.github/workflows/skills-trending.yml`:

```yaml
schedule:
  - cron: '0 2 * * *'  # UTC 02:00 = 北京时间 10:00
```

Cron 格式:
- `0 2 * * *` = 每天 10:00
- `0 */6 * * *` = 每 6 小时
- `0 0 * * 1` = 每周一 00:00

### 修改趋势阈值

创建 `.env` 文件并提交:

```bash
SURGE_THRESHOLD=0.5  # 50% 涨幅触发警报
DB_RETENTION_DAYS=60  # 保留 60 天数据
```

## 📊 查看数据

项目会自动创建以下文件:

- `data/trends.db` - SQLite 数据库
- `README.md` - 每日趋势报告
- `reports/` - HTML 报告目录

## 🔧 故障排查

### Actions 运行失败

1. 检查 Secrets 是否正确配置
2. 查看 Actions 日志中的错误信息
3. 确认 API Keys 是否有效

### 邮件未发送

1. 检查 `RESEND_API_KEY` 是否正确
2. 检查 `EMAIL_TO` 邮箱地址
3. 查看 Resend 控制板的发送记录

### 数据未更新

1. 检查 skills.sh 网站是否可访问
2. 查看 Playwright 是否正确安装
3. 检查网络连接

## 📧 邮件配置选项

### 方式 1: Resend (推荐)

```yaml
- name: Send Email via Resend
  env:
    RESEND_API_KEY: ${{ secrets.RESEND_API_KEY }}
    EMAIL_TO: ${{ secrets.EMAIL_TO }}
  run: |
    python src/resend_sender.py
```

### 方式 2: SMTP

```yaml
- name: Send Email via SMTP
  env:
    SMTP_HOST: smtp.gmail.com
    SMTP_PORT: 587
    SMTP_USER: ${{ secrets.SMTP_USER }}
    SMTP_PASSWORD: ${{ secrets.SMTP_PASSWORD }}
  run: |
    python src/smtp_sender.py
```

## 🎯 下一步

1. ✅ 配置 GitHub Secrets
2. ✅ 测试运行一次 Actions
3. ✅ 检查邮件是否正常发送
4. ✅ 等待第二天自动运行

## 📞 获取帮助

- 原项目: https://github.com/geekjourneyx/trending-skills
- 你的仓库: https://github.com/heelaw/trending-skills
- Issues: https://github.com/heelaw/trending-skills/issues

## 🎉 完成！

现在你已经有了一个自动运行的技能趋势追踪系统！
