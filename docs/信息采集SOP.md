---
status: active
---

# 信息采集 SOP

**核心理念**：注意力是稀缺资源。不追求"看完"，追求"关键信息快速提取 + 可回溯"。

---

## 一、采集流程

```
发现内容 → 丢链接到 Inbox
  ↓（集中处理时段）
① 提取内容（视频:抖虫 / 文章:Clipper）
  ↓
② AI 总结
  ↓
③ 写入信息源笔记（URL / 原文 / 总结）
  ↓
④ AI 读取信息源 → 输出汇报（含 [[wikilinks]]）
  ↓
⑤ 信息源移入 Archive
```

---

## 二、各步骤操作规范

### 0. Inbox — 刷到内容先丢链接

- 打开 `Inbox.md`
- 刷到感兴趣的内容，**只粘贴 URL**，一行一个
- 不做任何处理，不打断当前状态
- 目标：把"发现"和"处理"解耦

> Inbox 中的 URL 处理完毕后，标记为 `✅`。标记后不删除，保留记录。

### ① 提取内容

#### 视频 → 文案

- 去 https://www.dousnap.com/ 粘贴链接，获取完整文案
- 备用网站：[在线视频文案提取工具，一键提取视频文案 - 全平台抖音视频文案提取](https://www.transcriptgenerate.com/zh-CN)
- 快速扫读，判断是否值得进入下一步（价值过滤）

#### 文章/网页 → Markdown

- 用 [Obsidian Clipper](https://obsidian.md/clipper) 浏览器插件
- 点击 Clipper，自动提取网页结构转换为 Markdown
- 直接保存到本地 Obsidian 仓库
- 将保存后的文件从仓库根目录移入 `信息源/`

### ② AI 总结

#### 视频

- 去 https://www.dousnap.com/video-summary 粘贴链接，获取 AI 视频总结

#### 文章/Clipper 保存的网页

- 不需要额外总结步骤，Clipper 已提取结构化内容
- 如需精简摘要，可直接在 Obsidian 中让 AI 基于原文生成摘要，追加到笔记末尾

### ③ 写入信息源笔记 — 统一元数据格式

所有信息源必须使用 **Type A 元数据格式**（`title` / `source` / `created` / `description` / `tag` / `status`），不再使用抖音类简版格式。

```markdown
---
title: "{{文章标题或视频主题}}"
source: "{{原文链接}}"
created: {{采集日期 YYYY-MM-DD}}
description: "{{一句话摘要}}"
tag: ["{{标签1}}", "{{标签2}}"]
status: waiting
---

# {{原文 / 文案}}

{{抖虫文案 / Clipper 导出的 Markdown / 核心摘录}}

# 总结：

{{抖虫视频总结 / AI 生成摘要}}
```

字段说明：

| 字段 | 必填 | 说明 |
|------|------|------|
| `title` | 是 | 文章原名或视频主题概括 |
| `source` | 是 | 原文 URL 或视频链接 |
| `created` | 是 | 采集入库日期，格式 `YYYY-MM-DD` |
| `description` | 是 | 10-30 字一句话摘要 |
| `tag` | 是 | 标签数组，选取自下方标签体系 |
| `status` | 是 | `waiting`（待汇报）或 `reported`（已汇报）|

**标签体系**（从下列选取，可新增但需保持一致性）：

| 标签 | 适用场景 |
|------|---------|
| `AI编程` | Vibe Coding、Spec Coding、Cursor、Claude Code |
| `AI智能体` | Agent 框架（Hermes、OpenClaw、Harness） |
| `LLM工作流` | Prompt 工程、LLM 协作流程、上下文管理 |
| `视频创作` | Remotion、Motion、动画制作、剪映 |
| `学习` | 学习方法论、NotebookLM、知识管理 |
| `设计哲学` | 设计思想、范式、原则性讨论 |
| `领域驱动设计` | DDD、Ubiquitous Language、ADR |

**命名规则**：`{{核心主题}}.md`（不强制带平台前缀）
例：`什么是Vibe Coding.md`、`GrillMe到GrillWithDocs.md`

### ④ AI 汇报

AI 读取 `信息源/` 目录下的笔记后，按以下格式产出汇报：

- 每条信息标注来源（[[视频笔记名]] 双链）
- 跨笔记提炼共性模式
- 给出可执行的行动建议

汇报完成后，将该信息源笔记的 frontmatter 中 `status` 改为 `reported`。

### ⑤ 归档 Archive — 自动补标签 + 移入 Archive

**前置步骤（AI 在生成汇报时执行）：**

- 检查每条信息源的 `tag` 字段，如为空则按内容主题从标签体系中选取补全
- 填入 `tag: ["标签1", "标签2"]` 数组格式
- 同时补全 `created`（如缺失）、`description`（如缺失）、`title`（如缺失），确保所有字段为 Type A 完整格式

**归档操作：**

- 已汇报过的信息源笔记从 `信息源/` 移入 `Archive/{{归档年月}}/`（如 `Archive/2026-06/`）
- Inbox 中对应该内容的 URL 标记为 `✅`
- 信息汇报保留在 `信息汇报/`，不移入 Archive

> 原则：信息源是"正在处理"，Archive 是"已完结"。按月份归档，方便回溯。

---

## 三、触发时机 — 什么时候跑 AI 汇报

- **定期**：每周日跑一次，把当周积攒的 waiting 内容一并汇报
- **按量**：或者信息源攒到 5 条以上就跑一次
- **按需**：急需了解某个主题时，手动触发

---

## 四、Archive 回迁

- 如需重新使用 Archive 中的旧信息源，将其移回 `信息源/`，`status` 改回 `waiting`
- 下次 AI 汇报时会一并纳入

---

## 五、价值过滤原则

不是每条内容都值得走完5步。在步骤①后快速判断：

| 判断           | 动作                     |
| ------------ | ---------------------- |
| 看完觉得水/无新信息   | 丢弃，Inbox 标记 `❌`，不进入下一步 |
| 有1-2个亮点但整体一般 | 只写 URL+总结，不存全文         |
| 高质量信息        | 完整走完流程（①→⑤），进 AI 汇报    |

---

## 六、AI 汇报 Prompt 模板

```markdown
请完成以下任务：

**1. 汇报** — 阅读 `信息源/` 目录下的所有笔记，输出一份信息汇报：
  - 每条信息核心观点（附 [[笔记名]] 来源链接）
  - 跨信息共性模式或矛盾点
  - 对我有价值的行动建议
  - 哪些值得深入跟进

**2. 补元数据** — 汇报中用到的每条信息源笔记，检查 frontmatter：
  - `tag` 为空则按内容主题补标签（从标签体系选，数组格式）
  - `description` 为空则补一句话摘要
  - `created` 缺失则填当天日期
  - 统一为 Type A 格式（title / source / created / description / tag / status）

**3. 标记** — 汇报中用到的每条信息源笔记，将其 frontmatter 中 `status` 字段改为 `reported`。

**4. 清理** — 汇报中用到的信息源笔记，从 `信息源/` 移入 `Archive/{{当前年月}}/`。Inbox 中对应 URL 标记 `✅`。

**5. 输出** — 将汇报内容写入 `信息汇报/` 目录，文件名格式 `YYYY-MM-DD-主题.md`。
```

---

## 七、目录结构

```
vault 根目录/
├── Inbox.md                  ← 刷到内容先丢 URL
├── 信息源/                   ← 正在处理的笔记（status: waiting）
├── 信息汇报/                 ← AI 产出的分析汇报
├── Archive/                  ← 已汇报完结的信息源（按月份归档）
│   └── 2026-06/              ← 月份子目录
│       ├── 什么是Vibe Coding？.md
│       └── ...
├── 信息采集SOP.md            ← 本 SOP
```
