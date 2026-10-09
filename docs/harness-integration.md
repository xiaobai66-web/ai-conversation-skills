# Harness 集成指南

本文档说明如何在 DeepSeek Harness 中安装和使用这两个 skill。

---

## 🎯 目标

让 Harness 在检测到符合条件的用户输入时，自动加载对应的 skill，而不需要用户每次手动说 `skill("intent-clarification")`。

---

## 📦 安装方式

### 桌面版 Harness（推荐）

**这是大多数用户使用的版本**——通过桌面应用程序运行的 Harness。

#### 1. 确认 Skill 扫描目录

桌面版 Harness 会扫描以下目录：

```bash
C:\Users\<你的用户名>\.dsh\skills\
```

#### 2. 创建目录结构

**重要：** 桌面版需要 **目录格式**（`skill名称/SKILL.md`），不是单个 `.md` 文件。

```bash
C:\Users\<你的用户名>\.dsh\skills\
├── intent-clarification\
│   └── SKILL.md
└── causal-factor-analysis\
    └── SKILL.md
```

#### 3. 复制文件

- 复制 `skills/intent-clarification-codex.md` → `C:\Users\<你的用户名>\.dsh\skills\intent-clarification\SKILL.md`
- 复制 `skills/causal-factor-analysis-codex.md` → `C:\Users\<你的用户名>\.dsh\skills\causal-factor-analysis\SKILL.md`

**为什么用 codex 版本？** 因为桌面版需要 YAML frontmatter 格式，codex 版本正好是这个格式。

#### 4. 验证安装

在 Harness 中开启新对话，检查系统提示词（System Prompt）中是否包含：

```
<available_skills>
- intent-clarification: ...
- causal-factor-analysis: ...
</available_skills>
```

看到这两个 skill 名称即表示安装成功。

---

### 网页版 Harness（源码开发）

**仅用于开发者从源码运行 Harness 时使用。**

#### 1. 复制文件

复制 `skills/intent-clarification-harness.md` 和 `skills/causal-factor-analysis-harness.md` 到你的 Harness 源码的 `skills/` 目录。

#### 2. 格式说明

网页版使用 markdown 标题格式（无 YAML frontmatter）。

---

## ⚙️ 自动触发机制

### 桌面版如何工作

一旦 skill 正确安装到 `C:\Users\<你的用户名>\.dsh\skills\`，Harness 会：

1. ✅ 在系统提示词中包含 skill 列表
2. ✅ AI 根据 skill 内部定义的触发条件判断是否调用
3. ✅ 符合条件时自动加载对应的 skill

**无需额外配置**——skill 的触发逻辑已经内置在 skill 文件本身。

### 触发条件示例

**intent-clarification 会在以下情况触发：**
- 用户说话模糊（"我想做个..."）
- 有多种合理理解（3+ 种）
- 涉及高风险决策（金钱、法律、健康）
- 跨领域探索（用户明确说不懂）

**causal-factor-analysis 会在以下情况触发：**
- 目标已明确但需要理解"为什么"
- 陌生领域需要因果分析
- 重大决策需要清晰的因素分解
- 需要评估多个选项的权衡

---

## 🧪 验证安装

### 测试 1: 检查 Skill 是否被加载

在 Harness 中开启新对话，查看系统提示词（System Prompt）。

**期望结果：**
```
<available_skills>
- intent-clarification: 在 AI 回答或执行前，从用户的一句模糊表达中识别多种可能的意图...
- causal-factor-analysis: 当目标明确后，识别所有"决定性因素"...
</available_skills>
```

✅ 看到这两个 skill → 安装成功  
❌ 没有看到 → 检查目录结构和文件名是否正确

---

### 测试 2: intent-clarification 自动触发

**输入：**
```
我想做个任务管理 skill
```

**期望行为：**
- AI 先分析这个请求的多种可能理解
- 列出 2-4 种候选方向（任务提醒？对话交接？任务日志？依赖管理？）
- 问一个关键问题确认你的真实意图

---

### 测试 3: causal-factor-analysis 触发

**输入：**
```
我想开个线上课程，但不知道能不能赚钱
```

**期望行为：**
- AI 识别出需要深度分析
- 列出决定性因素（市场需求、课程质量、营销能力、定价策略...）
- 深度解释每个因素的因果关系（什么、为什么重要、如何影响、何时成立/不成立）

---

### 测试 4: 不应该触发

**输入：**
```
现在几点？
```

**期望行为：**
- AI 直接回答
- 不调用任何 skill

---

## 🔧 故障排查

### 问题 1: Skill 没有出现在 available_skills 列表

**可能原因：**
- 目录结构不对（必须是 `skill名称/SKILL.md` 格式）
- 文件名不对（必须是 `SKILL.md`，大小写敏感）
- 放错位置（必须在 `C:\Users\<你的用户名>\.dsh\skills\`）

**解决方案：**
1. 检查完整路径：
   ```
   C:\Users\<你的用户名>\.dsh\skills\intent-clarification\SKILL.md
   C:\Users\<你的用户名>\.dsh\skills\causal-factor-analysis\SKILL.md
   ```

2. 确认文件不是空的（至少有 YAML frontmatter）

3. 重启 Harness

---

### 问题 2: Skill 已加载但不自动触发

**可能原因：**
- 你的输入不符合触发条件
- Skill 内部的触发逻辑需要调整

**临时解决方案：**
手动调用 skill：
```
skill("intent-clarification")
```

**检查方法：**
- 查看 skill 文件中的触发条件说明
- 尝试更明显的模糊输入（如"我想做点什么但不知道从哪开始"）

---

### 问题 3: AI 说"skill 不存在"

**可能原因：**
- Skill 没有正确加载
- 文件格式错误（YAML frontmatter 格式不对）

**解决方案：**
1. 检查 YAML frontmatter 是否完整：
   ```yaml
   ---
   name: intent-clarification
   description: ...
   ---
   ```

2. 确认文件编码是 UTF-8

3. 检查是否有语法错误（YAML 对缩进敏感）

---

## 📊 桌面版 vs 网页版对比

| 特性 | 桌面版 Harness | 网页版 Harness（源码） |
|------|---------------|----------------------|
| **安装位置** | `C:\Users\<用户名>\.dsh\skills\` | `<源码根目录>\skills\` |
| **目录格式** | `skill名称/SKILL.md` | 单个 `.md` 文件 |
| **文件格式** | YAML frontmatter | markdown 标题 |
| **使用文件** | `*-codex.md` 版本 | `*-harness.md` 版本 |
| **重启需求** | 是（修改后需重启） | 否（HMR 热更新） |
| **适用人群** | 所有用户 | 开发者 |

---

## 💡 使用技巧

### 手动触发

即使 skill 会自动触发，你也可以随时手动调用：

```
skill("intent-clarification")
skill("causal-factor-analysis")
```

### 跳过 Skill

如果你确定不需要 skill 介入，可以在请求中明确说明：

```
直接帮我写代码，不要调用 skill
```

### 调整触发条件

如果你觉得 skill 触发太频繁或太少，可以：

1. 编辑 `SKILL.md` 文件中的触发条件说明
2. 重启 Harness 让修改生效

---

## 📚 相关文档

- [意图澄清 Skill 文档](../skills/intent-clarification-codex.md)
- [因果分析 Skill 文档](../skills/causal-factor-analysis-codex.md)
- [设计原理](design-rationale.md)
- [对比分析](comparison.md)

---

## 🆘 需要帮助？

如果遇到问题，可以：

1. 检查 Harness 日志（通常在 `C:\Users\<你的用户名>\.dsh\logs\`）
2. 在 GitHub 仓库提 Issue：https://github.com/xiaobai66-web/ai-intent-skills/issues
3. 查看完整的安装案例：[examples/](../examples/)

---

**更新日期：** 2026-10-09  
**兼容版本：** DeepSeek Harness 桌面版（测试环境）


