# GitHub + Obsidian 笔记系统详细说明

> 目标：解决你的困惑——文件夹怎么放、踩坑记录写哪、Obsidian怎么用

---

## 1. 核心问题：GitHub和Obsidian共用一个文件夹吗？

### 答案：是的，共用一个文件夹

```
你的电脑上只有一个文件夹：learning-notes

这个文件夹同时是：
├── GitHub仓库（可以git push到GitHub网站）
└── Obsidian笔记库（用Obsidian打开这个文件夹）
```

### 具体操作步骤

**第一步：创建GitHub仓库**
```
1. 打开 GitHub 网站
2. 点击 New Repository
3. 名称填：learning-notes
4. 描述填：Kay Gu's programming learning journey
5. 选择 Public
6. 勾选 "Add a README file"
7. 点击 Create repository
```

**第二步：克隆到本地**
```bash
# 在你想要放笔记的目录下执行
git clone https://github.com/heituanzi-jpg/learning-notes.git
```

**第三步：用Obsidian打开这个文件夹**
```
1. 打开 Obsidian
2. 点击 "打开文件夹作为库"
3. 选择刚才clone下来的 learning-notes 文件夹
4. 完成！现在你可以用Obsidian写笔记，写完后用Git提交到GitHub
```

### 关键：.gitignore 必须配置

在 learning-notes 文件夹根目录创建 `.gitignore` 文件，内容如下：

```gitignore
# Obsidian的配置文件夹（不需要上传到GitHub）
.obsidian/

# 系统文件
.DS_Store
Thumbs.db

# 临时文件
*.log
*.tmp
*.bak
```

这样Obsidian的配置不会被上传到GitHub，但你的笔记内容会。

---

## 2. 踩坑记录放哪里？

### 方案A：写在每日日志里（推荐，简单）

每天遇到的坑，直接写在当天的日志里：

**文件**：`daily-log/2026-04-19.md`

```markdown
# 2026-04-19 学习日志

## 今日目标
- [ ] 学习Git基础命令
- [ ] 改ranphicat官网首页

## 完成情况
- ✅ 学会了git add/commit/push
- ✅ 改了首页h1的字体大小

## 踩坑记录
- ❌ 忘记先git pull就push了，导致冲突
  - 解决：以后每次push前先git pull
- ❌ 修改CSS后网页没变化
  - 原因：浏览器缓存
  - 解决：Ctrl+F5 强制刷新

## 明日计划
- [ ] 学习CSS的flex布局
```

### 方案B：单独建立issues文件夹（适合重要问题）

如果某个坑特别重要，单独建一个文件：

**文件**：`project-notes/ranphicat-website/issues/2026-04-19-git-conflict.md`

```markdown
# Git冲突解决记录

## 问题描述
今天push时报错：fatal: unable to access... Connection was reset

## 原因分析
梯子不稳定，连接中断

## 解决方案
1. 检查梯子是否开启
2. 稍等几秒重新push
3. 如果反复失败，换个节点

## 预防措施
每次push前检查梯子状态
```

### 我的建议

**新手阶段**：用方案A，把踩坑记录写在每日日志里，简单直接。

**进阶阶段**：遇到特别重要的问题，再用方案B单独记录。

---

## 3. 文件夹结构和用途一览

```
learning-notes/                    ← GitHub仓库 + Obsidian笔记库（共用这一个文件夹）
│
├── .gitignore                     ← 告诉Git哪些文件不要上传
│
├── README.md                      ← GitHub仓库首页（介绍这个仓库是干嘛的）
│
├── daily-log/                     ← 每日学习日志
│   ├── 2026-04-19.md              ← 今天学了什么、踩了什么坑
│   ├── 2026-04-20.md              ← 明天学了什么
│   └── ...
│
├── code-snippets/                 ← 代码片段收集（以后可以复用）
│   ├── html/
│   │   ├── navbar.md              ← 导航栏代码模板
│   │   └── card.md                ← 卡片布局代码模板
│   ├── css/
│   │   ├── flex-center.md         ← Flex居中代码
│   │   └── hover-effect.md        ← 悬停效果代码
│   └── javascript/
│       └── ...
│
├── project-notes/                 ← 项目笔记（每个项目一个文件夹）
│   ├── ranphicat-website/
│   │   ├── setup.md               ← 项目怎么搭建的
│   │   ├── structure.md           ← 项目结构说明
│   │   └── issues/                ← 遇到的重要问题
│   │       └── git-conflict.md
│   └── ...
│
└── knowledge/                     ← 知识点深度笔记（用Obsidian的双向链接）
    ├── html/
    │   ├── div和span的区别.md
    │   └── 语义化标签.md
    ├── css/
    │   ├── Flexbox布局.md
    │   └── 盒模型.md
    └── git/
        ├── 基本命令.md
        └── 分支管理.md
```

---

## 4. 每天怎么用这套系统？

### 早上（开始学习前）

```
1. 打开Obsidian
2. 在 daily-log 文件夹新建今天的日志文件（如 2026-04-19.md）
3. 写下今天的"今日目标"
4. 打开ranphicat-website项目，开始改代码
```

### 学习过程中

```
1. 学到一个新知识点 → 在 knowledge 文件夹写一篇笔记
2. 写了一段有用的代码 → 在 code-snippets 保存下来
3. 踩了一个坑 → 记在当天的 daily-log 里
4. 重要问题 → 在 project-notes/issues 单独建文件
```

### 晚上（学习结束前）

```
1. 回到 daily-log，更新"完成情况"
2. 写下"明日计划"
3. 打开终端，提交今天的笔记到GitHub：

   cd learning-notes
   git add .
   git commit -m "docs: 2026-04-19 学习日志 + Flexbox笔记"
   git push
```

### 每周五晚上

```
打开 Obsidian，回顾本周写的所有笔记
- 看看哪些知识点真正理解了
- 标记还需要深入的地方
- 整理代码片段，删除重复的
```

---

## 5. Obsidian的核心功能怎么用？

### 双向链接（最强大的功能）

在笔记里用 `[[文件名]]` 创建链接：

```markdown
今天学习了 [[Flexbox布局]]，用到了 [[justify-content]] 和 [[align-items]]。

遇到的问题参考 [[git-conflict解决]]。
```

这样点击链接就能跳转到对应笔记，Obsidian会自动生成反向链接。

### 标签

在笔记开头添加标签：

```markdown
---
tags: [css, layout, flex]
created: 2026-04-19
---
```

以后可以用标签搜索所有相关笔记。

### 模板

Obsidian可以创建模板，每天新建日志时自动套用：

1. 在Obsidian设置里开启"模板"插件
2. 创建模板文件夹：`templates/`
3. 创建日志模板：`templates/daily-log.md`

```markdown
# {{date}} 学习日志

## 今日目标
- [ ] 
- [ ] 

## 完成情况
- 

## 踩坑记录
- 

## 明日计划
- [ ] 
```

4. 每天新建日志时，用模板自动填充

---

## 6. 总结：一句话说清楚

| 问题 | 答案 |
|------|------|
| GitHub和Obsidian共用文件夹吗？ | **是的**，learning-notes既是GitHub仓库，也是Obsidian笔记库 |
| 踩坑记录放哪？ | **写在每日日志里**，重要问题才单独建文件 |
| Obsidian深度笔记是什么？ | **就是learning-notes/knowledge/文件夹里的笔记**，用双向链接关联 |
| 每天怎么做？ | **早上写目标 → 学习中记笔记 → 晚上提交GitHub** |
| Git怎么同步？ | **写完笔记后 git add . → git commit → git push** |

---

## 7. 快速上手清单

- [ ] 在GitHub创建 learning-notes 仓库
- [ ] 克隆到本地
- [ ] 创建 .gitignore 文件
- [ ] 创建文件夹结构（daily-log, code-snippets, project-notes, knowledge）
- [ ] 用Obsidian打开 learning-notes 文件夹
- [ ] 创建今天的日志文件
- [ ] 开始学习，边学边记
- [ ] 晚上提交到GitHub
