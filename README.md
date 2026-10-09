# 🎯 AI Intent Skills

> Two skills that help AI understand what you actually want before acting.

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://github.com/xiaobai66-web/ai-intent-skills)

---

## 💡 What Problem Does This Solve

You say **"I want to buy stocks"**. AI might think you mean:
- Teach me the basics
- Recommend specific stocks
- Help me open an account
- Judge if now is a good time
- Analyze if this idea makes sense

**If AI picks wrong, the whole conversation goes sideways.**

You say **"I want to do AI e-commerce"**. AI might give you a plan immediately, but:
- Doesn't explain *why* certain directions work
- Doesn't tell you *when* the advice breaks down
- Doesn't distinguish facts from guesses
- Doesn't show you how to verify quickly

**You end up learning for months without knowing if it's even viable.**

---

## 🔧 Two Skills

<table>
<tr>
<td width="50%" valign="top">

### 🎤 Intent Clarification

Figures out what you actually want before answering.

**Core Features:**
- Lists 2-4 possible interpretations
- Shows evidence for each
- Asks *one* key question to confirm
- Forms "provisional goal" you can correct anytime

**Use it when:**  
Vague request, multiple meanings, high-risk decisions

[Read the skill →](skills/intent-clarification-codex.md)

</td>
<td width="50%" valign="top">

### 🔍 Causal Factor Analysis

Breaks down "what determines success" with deep explanations.

**Core Features:**
- Identifies decisive factors (things that actually change outcomes)
- Explains *why* and *how*, not just *what*
- Uses concrete examples for real scenarios
- Marks fact vs. assumption vs. unknown
- Tells you *when* advice stops working
- Gives minimal validation plan

**Use it when:**  
Clear goal but unfamiliar domain, need to evaluate viability

[Read the skill →](skills/causal-factor-analysis-codex.md)

</td>
</tr>
</table>

---

## 🤔 Why Two Skills

**Different jobs, different triggers.**

**Intent Clarification:** Vague input → Confirmed provisional goal → Just enough to get direction right  
**Causal Factor Analysis:** Clear goal but unfamiliar domain → Deep causal breakdown + validation plan → Full explanation of decisive factors

Combining them made each half-baked. Separating lets each do its job properly.

---

## 🔄 How They Work Together

```
You: "I want to buy stocks"
    ↓
Intent Clarification:
  "I see 4 possibilities... which one?"
    ↓
You: "I want to learn, then buy a small amount"
    ↓
Causal Factor Analysis:
  "Here's what determines success:
   - Market selection (why: affects regulations, costs...)
   - Risk tolerance (why: determines position size...)
   - Account setup (why: affects speed...)
   
   Each factor explained with:
   ✅ What's known
   ❓ What's unknown
   ⚠️ What's assumed
   🔄 When this changes"
```

---

## 📦 Installation

### 💻 Codex
Copy `skills/intent-clarification-codex.md` and `skills/causal-factor-analysis-codex.md` to your Codex skills folder.

### 🖥️ Harness (Desktop)
Copy files to `C:\Users\<YourUsername>\.dsh\skills\`, directory format:

```
📁 C:\Users\<YourUsername>\.dsh\skills\
├── 📁 intent-clarification\
│   └── 📄 SKILL.md
└── 📁 causal-factor-analysis\
    └── 📄 SKILL.md
```

**Usage:** Once installed, AI will automatically load the corresponding skill based on your input. You can also manually invoke `skill("intent-clarification")`

📖 See [Harness Integration Guide](docs/harness-integration.md) for details

---

## ⚖️ What Makes This Different

| Comparison | Regular AI | This Project |
|------------|------------|--------------|
| **Follow-up Questions** | Asks more questions | *Shows* how AI interprets your words |
| **Task Breakdown** | Gives you steps | Gives you *causality* (why it matters, how it affects, when it fails) |
| **Existing Tools** | Rasa: doesn't let you choose<br>PMAgent: only for PM scenarios<br>TypeChat: no probability ranking | Candidate ranking + User choice + Causal explanation + Provisional goals + Reversal conditions |

[See full comparison →](docs/comparison.md)

---

## ✅ Real Testing

**Stock Investment:** "I want to learn how to buy stocks from scratch" → One conversation from vague idea to clear path (9.0/10)

**Agent Configuration:** "I'm seeing agent tutorials everywhere, feeling like I need to standardize my usage" → User went from "completely don't understand" to full understanding (9.66/10)

[See full examples →](examples/)

---

## 📌 More

**Design Philosophy:** From real conversations, not theory · [Full design story →](docs/design-rationale.md)

**Roadmap:** v1.0 (intent clarification + causal breakdown) → v1.1 (understanding check + dynamic priority) → v2.0 (visual causal graphs)

**License:** MIT

---

**GitHub:** https://github.com/xiaobai66-web/ai-intent-skills
