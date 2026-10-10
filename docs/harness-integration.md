# Claude Code 集成指南

本文档说明如何在 Claude Code 中安装和使用这两个 skill。

---

## 🎯 目标

让 Claude Code 在检测到符合条件的用户输入时，自动加载对应的 skill，而不需要每次手动调用。

---

## 📦 安装方式

### Claude Code（CLI / 桌面版 / IDE 插件）

#### 1. 确认 Skill 目录

Claude Code 从以下位置扫描 skill：

```
# 全局（所有项目可用）
C:\Users\<你的用户名>\.claude\skills\

# 项目级（只在当前项目可用）
<项目根目录>\.claude\skills\
```

#### 2. 创建目录结构

每个 skill 放在独立子目录下，文件名固定为 `SKILL.md`：

```
.claude\skills\
├── intent-clarification\
│   └── SKILL.md
└── causal-factor-analysis\
    └── SKILL.md
```

#### 3. 复制文件

- 复制 `skills/intent-clarification-codex.md` → `.claude\skills\intent-clarification\SKILL.md`
- 复制 `skills/causal-factor-analysis-codex.md` → `.claude\skills\causal-factor-analysis\SKILL.md`

**为什么用 codex 版本？** codex 版本包含 YAML frontmatter，Claude Code 靠它识别 skill 名称和描述。harness 版本是纯文档格式，没有 frontmatter，无法被自动加载。

#### 4. 验证安装

在 Claude Code 中开启新对话，输入：

```
/intent-clarification
```

如果 skill 正确加载，AI 会按照 skill 的工作流运行。

---

## ⚙️ 触发机制

### 自动触发

skill 内部定义了触发条件。安装后，AI 会根据输入判断是否调用：

- `intent-clarification`：输入模糊、有多种理解、高风险决策时自动触发
- `causal-factor-analysis`：目标明确后，需要理解"为什么"和因果关系时触发

### 手动调用

任何时候都可以手动触发：

```
/intent-clarification
/causal-factor-analysis
```

---

## 🧪 验证安装

### 测试 1：intent-clarification 自动触发

**输入：**
```
我想做个任务管理 skill
```

**期望行为：**
- AI 先分析这个请求的多种可能理解
- 列出 2-4 种候选方向
- 问一个关键问题确认真实意图

### 测试 2：causal-factor-analysis 触发

**输入：**
```
我想开个线上课程，但不知道能不能赚钱
```

**期望行为：**
- AI 识别出需要深度分析
- 列出决定性因素（市场需求、课程质量、营销能力、定价...）
- 深度解释每个因素的因果关系

### 测试 3：不应该触发

**输入：**
```
现在几点？
```

**期望行为：**
- AI 直接回答，不调用任何 skill

---

## 🔧 故障排查

### Skill 没有被识别

**可能原因：**
- 目录结构不对（必须是 `skill名称/SKILL.md`）
- 文件名不对（必须是 `SKILL.md`，大小写敏感）
- 用错了版本（应该用 `*-codex.md`，不是 `*-harness.md`）
- 放在了错误位置

**检查清单：**
```
# 全局安装路径（Windows）
C:\Users\<用户名>\.claude\skills\intent-clarification\SKILL.md
C:\Users\<用户名>\.claude\skills\causal-factor-analysis\SKILL.md

# 或项目级安装路径
<项目根目录>\.claude\skills\intent-clarification\SKILL.md
<项目根目录>\.claude\skills\causal-factor-analysis\SKILL.md
```

**验证文件有 frontmatter：** 打开 `SKILL.md`，确认文件开头有：
```yaml
---
name: intent-clarification
description: ...
---
```

### Skill 已加载但不自动触发

**临时解决方案：** 手动调用 `/intent-clarification`

**根本原因：** 你的输入不符合触发条件。尝试更明显的模糊输入，如"我想做点什么但不知道从哪开始"。

---

## 📊 文件版本说明

| 文件 | 格式 | 用途 |
|------|------|------|
| `*-codex.md` | YAML frontmatter + 中文内容 | Claude Code 安装版本 ✅ |
| `*-harness.md` | 纯 Markdown | 英文参考文档，供阅读和二次开发 |

---

## 💡 使用技巧

### 跳过 Skill

如果不需要 skill 介入，直接说明：

```
直接帮我写代码，不要调用 skill
```

### 两个 Skill 协同

标准工作流：

```
用户输入模糊
  → /intent-clarification 澄清意图，形成暂定目标
  → /causal-factor-analysis 深度拆解决定性因素
  → 执行/规划/研究
```

### 调整触发条件

编辑安装目录下的 `SKILL.md` 文件，修改触发条件部分，保存后在新对话中生效。

---

**更新日期：** 2026-10-10  
**兼容版本：** Claude Code CLI、桌面版、VS Code / JetBrains 插件
