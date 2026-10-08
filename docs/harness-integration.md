# Harness 集成指南

本文档说明如何在 DeepSeek Harness 中启用这两个 skill 的自动触发。

---

## 🎯 目标

让 Harness 在检测到符合条件的用户输入时，自动加载对应的 skill，而不需要用户每次手动说 `skill("intent-clarification")`。

---

## ⭐ 推荐方案：使用 WORKSPACE_INSTRUCTIONS.md

**最简单、最灵活的方式**——不需要修改 Harness 源码，不需要重新构建，**立即生效**。

### 步骤

1. **复制模板文件到你的工作目录：**

```bash
cp templates/WORKSPACE_INSTRUCTIONS.md /你的工作目录/
```

或直接从 [templates/WORKSPACE_INSTRUCTIONS.md](../templates/WORKSPACE_INSTRUCTIONS.md) 复制内容。

2. **完成！**

Harness 会在每次对话开始时自动读取这个文件，AI 会根据里面的规则判断是否需要调用 skill。

### 工作原理

- ✅ Harness 启动新对话时自动读取 `WORKSPACE_INSTRUCTIONS.md`
- ✅ AI 将文件内容作为工作区全局规则
- ✅ AI 根据触发条件自动调用对应的 skill
- ✅ 修改文件后，下次对话立即生效

### 优点

- 🚀 **零配置**：不需要修改 Harness 源码
- 🔥 **即时生效**：修改后立即应用于新对话
- 🎯 **灵活调整**：随时修改触发条件
- 📁 **项目隔离**：每个项目可以有自己的规则

---

## 备选方案：修改 Harness 系统提示词

**仅当你需要全局生效（所有工作目录）时使用此方案。**

⚠️ **注意：** 这种方式需要修改源码并重新构建 Harness，比较复杂。推荐使用上面的 WORKSPACE_INSTRUCTIONS.md 方案。

### 📝 修改步骤

### 1. 找到系统提示词文件

文件位置：
```
D:\Agent兄弟会\harness\packages\core\system-prompt\src\index.ts
```

### 2. 添加自动触发逻辑

在 `harness:independent-judgment` section 之后（约在 394 行），添加以下代码：

```typescript
// Skill auto-triggering logic
this.section({
  name: 'harness:skill-triggers',
  order: -98,
  text: `## Skill Auto-Triggering

When user input matches the following patterns, load the corresponding skill BEFORE answering:

### intent-clarification
Load this skill when the user's request is ambiguous or has multiple valid interpretations:

**Trigger conditions:**
- Vague goals: "I want to do something" / "I'm thinking about..." / "I need to..."
- Needs decomposition: "don't know how to..." / "not sure where to start..." / "need help figuring out..."
- Multiple reasonable interpretations: the same input could mean 3+ different things
- High-risk decisions: involves money, legal, health, career, business, or long-term commitments
- Cross-domain: user explicitly states unfamiliarity with the domain

**Do NOT trigger for:**
- Simple factual questions: "What time is it?" / "How do I read a file in Python?"
- Clear execution requests: "Write a function for me" / "Fix this bug"
- Chat acknowledgments: "OK" / "Continue" / "Thanks"

**Gray area (judge by context):**
- "I want to learn X": trigger if complete beginner, simplify if experienced
- "Help me evaluate this idea": trigger (needs goal clarification)
- "How to do this project": trigger if complex, don't trigger for small features

**How to use:**
When triggered, call \`skill("intent-clarification")\` first, then follow its workflow to clarify the user's actual intent before proceeding.

### causal-factor-analysis
Load this skill when the goal is clear but needs deep analysis of decisive factors:

**Trigger conditions:**
- Goal is confirmed but user needs to understand "why" and "how"
- Unfamiliar domain requiring causal understanding
- Major decision requiring clear factor breakdown
- Need to evaluate multiple options with tradeoff analysis
- User asks "what do I need to pay attention to" / "what are the key factors"

**How to use:**
After intent is clarified (either by intent-clarification skill or already clear), call \`skill("causal-factor-analysis")\` to identify and decompose decisive factors.

**Workflow coordination:**
1. If user input is ambiguous → use intent-clarification first
2. Once intent is clear → use causal-factor-analysis for deep breakdown
3. Finally → proceed to execution/research/planning based on the analysis

**Example:**
User: "I want to make a task management skill"
→ This is vague (what kind of task management? reminders? handoff? logs?)
→ Load intent-clarification first
→ After clarifying: they want conversation handoff to prevent drift
→ Load causal-factor-analysis to break down key factors
→ Then proceed with implementation`,
})
```

### 3. 重新构建 Harness

在 Harness 根目录执行：

```powershell
cd D:\Agent兄弟会\harness
pnpm run build
```

或使用完整路径：

```powershell
& "C:\Users\ASUS\.dsh\dsh-runtimes\dsh-primary-runtime\dependencies\node\bin\node.exe" `
  "C:\Users\ASUS\.dsh\dsh-runtimes\dsh-primary-runtime\dependencies\pnpm\bin\pnpm.mjs" `
  run build
```

### 4. 重启 Harness

构建完成后，重启 DeepSeek Harness 让修改生效。

---

## ✅ 验证

修改生效后，测试以下场景：

### 测试 1: intent-clarification 自动触发

**输入：**
```
我想做个任务管理 skill
```

**期望行为：**
- AI 先调用 `skill("intent-clarification")`
- 列出 2-4 种可能的理解（任务提醒？对话交接？任务日志？）
- 问一个关键问题确认方向

### 测试 2: causal-factor-analysis 自动触发

**输入：**
```
我想开个线上课程，但不知道能不能赚钱
```

**期望行为：**
- AI 识别出需要深度分析
- 调用 `skill("causal-factor-analysis")`
- 列出决定性因素（市场需求、课程质量、营销能力...）
- 深度解释每个因素的因果关系

### 测试 3: 不应该触发

**输入：**
```
现在几点？
```

**期望行为：**
- AI 直接回答
- 不调用任何 skill

---

## 🔧 故障排查

### 问题：构建失败

**可能原因：** pnpm 命令未找到

**解决方案：** 使用完整路径（见步骤 3）

### 问题：修改后没有生效

**检查清单：**
1. ✅ 确认 `index.ts` 文件已保存
2. ✅ 确认构建成功完成（无错误）
3. ✅ 确认已重启 Harness
4. ✅ 确认 skill 文件已正确安装在 `D:\Agent兄弟会\harness\skills\`

### 问题：AI 过度触发 skill

**调整方案：**

修改 `order` 值（数字越小优先级越高）：
- 当前：`order: -98`
- 降低优先级：改为 `order: -90` 或更大的值

或在触发条件里添加更严格的限制。

---

## 📚 相关文档

- [意图澄清 Skill 文档](../skills/intent-clarification-harness.md)
- [因果分析 Skill 文档](../skills/causal-factor-analysis-harness.md)
- [Harness 系统提示词文档](https://github.com/deepseek-ai/dsh)

---

## 🆘 需要帮助？

如果遇到问题，可以：

1. 检查 Harness 日志（通常在 `~/.dsh/logs/`）
2. 在 GitHub 仓库提 Issue
3. 临时禁用自动触发：注释掉 `harness:skill-triggers` section

---

**更新日期：** 2026-10-08  
**兼容版本：** DeepSeek Harness ≥ 0.1.1-rc.1
