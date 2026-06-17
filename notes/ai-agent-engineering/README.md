# AI Agent 工程：Harness Design 三篇核心文献

三篇来自 OpenAI 和 Anthropic 的官方工程博客，主题一致：**如何设计 agent harness（驾驭框架）让 AI 智能体进行长期、自主的软件开发**。

---

## 文章列表

| # | 来源 | 标题 | 发布日期 |
|---|------|------|---------|
| 1 | Anthropic | Effective harnesses for long-running agents | 2025.11 |
| 2 | Anthropic | Harness design for long-running application development | 2026.3 |
| 3 | OpenAI | 工程技术：在智能体优先的世界中利用 Codex | 2026 |

---

## 演进路线

```
Anthropic ① → Anthropic ② → OpenAI
两代理模式   → 三代理GAN式  → 全代理团队
初始化器+编码 → 规划+生成+评估 → 0行人工代码
```

## 关键共识

1. **评估必须分离**：agent 自己评自己做不好，会自信地称赞烂活
2. **知识在仓库里**：agent 访问不到的 = 不存在，AGENTS.md 是目录不是百科全书
3. **架构约束是前提**：agent 团队比人类团队更早需要严格的架构纪律
4. **AI slop 需要垃圾回收**：编码黄金原则 → 后台 agent 扫描 → 自动修复
