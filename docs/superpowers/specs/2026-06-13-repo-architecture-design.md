# DevPatterns 仓库架构设计

## 背景

DevPatterns 是一个私有文档仓库，两人维护（HP-Patience、voidzc），存储开发模式、架构范式、工具配置等笔记。当前仓库只有一篇文档和 16 张截图，没有目录结构，需要建立可持续的架构。

## 内容分类

1. **前端设计流程** — AI 工具搭建落地页工作流、组件模式、前端范式
2. **后端/架构模式** — 后端设计模式、架构决策记录
3. **工具/环境配置** — Git 工作流、开发环境搭建、工具指南
4. **项目管理** — 分支规范、协作流程、项目约定

## 目录结构

```
DevPatterns/
├── README.md                    # 仓库概览 + 目录索引
├── CLAUDE.md                    # Claude Code 项目指令（写法约定）
├── .gitignore                   # 忽略系统文件、编辑器临时文件
│
├── frontend/                    # 前端相关
│   ├── README.md                # 本目录索引
│   ├── 前端设计流程.md
│   └── images/                  # 仅前端相关图片
│
├── backend/                     # 后端/架构模式
│   ├── README.md
│   └── images/
│
├── tools/                       # 工具/环境配置
│   ├── README.md
│   └── images/
│
├── project-management/          # 项目管理规范
│   ├── README.md
│   └── images/
│
└── docs/                        # 仓库自身相关的文档
    └── superpowers/
        └── specs/               # 设计文档存放
```

## 文件规范

### README.md

顶层 README 做"地图"，列出所有主题目录 + 一句话简介。每个子目录的 README 列出本目录包含哪些文档及其用途。

### CLAUDE.md 内容

```markdown
# DevPatterns

## 语言
- 笔记主体用中文
- 专业术语、代码、命令保留英文原样
- 文件名使用有意义的中文或英文，保持一致

## 文件命名
- 描述性名称，如 `前端设计流程.md`
- 避免无意义编号（`note1.md`、`final_v3.md`）

## 图片
- 就近放入同级 `images/` 目录
- 截图建议压缩后再提交（GitHub 不擅长管理大二进制文件）
- 文件名简短有意义

## 协作
- 私有仓库，灵活处理
- 直接推送 main 或 PR 均可
```

### .gitignore

```
# OS
.DS_Store
Thumbs.db

# Editor
*.swp
*.swo
*~

# IDE
.vscode/
.idea/
*.iml
```

## 迁移计划

一次性操作：

1. 创建 `frontend/` 目录
2. 将 `前端设计流程.md` 移动到 `frontend/`
3. 将根目录 `images/` 移动到 `frontend/images/`
4. 创建顶层 README.md、CLAUDE.md、.gitignore
5. 提交并推送

## 后续扩展

- 增加新内容：直接在对应主题目录下创建 .md 文件，必要时创建 `images/`
- 新主题类别：在根目录创建新目录 + README.md
- 超过 5 个主题目录时，考虑是否需要次级分类
