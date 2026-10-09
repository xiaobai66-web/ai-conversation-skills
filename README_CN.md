# 🎯 AI 意图技能

> 两个技能，让 AI 在行动前先搞清楚你想要什么。

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/xiaobai66-web/ai-intent-skills)
[![GitHub Stars](https://img.shields.io/github/stars/xiaobai66-web/ai-intent-skills?style=social)](https://github.com/xiaobai66-web/ai-intent-skills/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/xiaobai66-web/ai-intent-skills?style=social)](https://github.com/xiaobai66-web/ai-intent-skills/network/members)

**关键词：** AI Agent · 意图识别 · 因果分析 · Prompt Engineering · ChatGPT · Claude · LangChain · 对话系统

---

## 💡 解决什么问题

你说 **"我想买股票"**，AI 可能理解成：
- 教我基础知识
- 推荐具体股票
- 帮我开户
- 判断现在是不是好时机
- 分析这个想法是否靠谱

**猜错了，整个对话就偏了。**

你说 **"我想做 AI 电商"**，AI 可能马上给你方案，但：
- 不解释*为什么*某些方向可行
- 不告诉你*什么时候*建议会失效
- 不区分事实和猜测
- 不告诉你怎么快速验证

**学几个月才发现根本不可行。**

---

## 🔧 两个技能

<table>
<tr>
<td width="50%" valign="top">

### ✅ 意图澄清

回答前先搞清楚你到底想干什么。

**核心功能：**
- 列出 2-4 个可能的理解
- 展示每个理解的依据
- 问*一个*关键问题确认方向
- 形成"暂定目标"，随时可纠正

**何时用：**  
请求模糊、有多种理解、高风险决策

[查看技能 →](skills/intent-clarification-codex.md)

</td>
<td width="50%" valign="top">

### 🧩 因果分析

拆解"什么决定成败"并深度解释。

**核心功能：**
- 识别决定性因素（真正改变结果的）
- 解释*为什么*和*如何影响*
- 用具体例子让你想象实际场景
- 标注事实 vs 假设 vs 未知
- 告诉你*什么时候*建议会失效
- 给你最小化验证方案

**何时用：**  
目标明确但不懂领域，评估可行性

[查看技能 →](skills/causal-factor-analysis-codex.md)

</td>
</tr>
</table>

---

## 🤔 为什么分成两个

**分开后各自做好自己的事。**

**意图澄清：** 用户说话模糊 → 确认暂定目标 → 刚好能确认方向  
**因果分析：** 目标明确但不懂领域 → 深度因果拆解 + 验证方案 → 完整解释决定性因素

---

## 🔄 它们如何配合

```
你："我想买股票"
    ↓
意图澄清：
  "我想到 4 种可能... 哪一种？"
    ↓
你："我想先学习，然后买一点试试"
    ↓
因果分析：
  "这些因素决定成败：
   - 市场选择（为什么：影响监管、成本...）
   - 风险承受（为什么：决定仓位大小...）
   - 开户流程（为什么：影响速度...）
   
   每个因素都包含：
   ✅ 已知什么
   ❓ 未知什么
   ⚠️ 假设什么
   🔄 什么情况下改变"
```

---

## 📦 安装

### 💻 Codex
复制 `skills/intent-clarification-codex.md` 和 `skills/causal-factor-analysis-codex.md` 到你的 Codex 技能文件夹。

### 🖥️ Harness（桌面版）
复制文件到 `C:\Users\<你的用户名>\.dsh\skills\`，目录格式：

```
📁 C:\Users\<你的用户名>\.dsh\skills\
├── 📁 intent-clarification\
│   └── 📄 SKILL.md
└── 📁 causal-factor-analysis\
    └── 📄 SKILL.md
```

**使用：** 安装后，AI 会根据输入自动加载对应的 skill。你也可以手动调用 `skill("intent-clarification")`

📖 详细安装说明见 [Harness 集成指南](docs/harness-integration.md)

---

## ⚖️ 有什么不同

| 对比项 | 普通 AI | 本项目 |
|--------|---------|--------|
| **追问方式** | 问更多问题 | *展示* AI 是怎么理解你的话 |
| **任务拆解** | 给你步骤 | 给你*因果关系*（为什么重要、如何影响、何时失效） |
| **现有工具** | Rasa：不让你选<br>PMAgent：只针对 PM<br>TypeChat：没有概率排序 | 候选排序 + 用户选择 + 因果解释 + 暂定目标 + 反转条件 |

[查看完整对比 →](docs/comparison.md)

---

## ✅ 真实测试

**股票投资：** "我想从零学会怎么买股票" → 一次对话从模糊想法到清晰路径

**Agent 配置：** "感觉我需要规范化 agent 用法" → 用户从"完全不懂"到完全理解

[查看完整案例 →](examples/)

---

## 📌 其他

**设计哲学：** 来自真实对话，不是理论 · [完整设计故事 →](docs/design-rationale.md)

**路线图：** v1.0（意图澄清 + 因果拆解）→ v1.1（理解检查 + 动态优先级）→ v2.0（可视化因果图）

**许可：** MIT

---

**GitHub:** https://github.com/xiaobai66-web/ai-intent-skills
