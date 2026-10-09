# AI Intent Skills

Two skills that help AI understand what you actually want before acting.

---

## What Problem Does This Solve

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

## Two Skills

### Intent Clarification
Figures out what you actually want before answering.

- Lists 2-4 possible interpretations of your words
- Shows you the evidence for each
- Asks *one* key question to confirm direction
- Forms a "provisional goal" you can correct anytime

**Use it when:** Your request is vague, has multiple meanings, or involves high-risk decisions.

[Read the skill →](skills/intent-clarification-codex.md)

### Causal Factor Analysis
Breaks down "what determines success" with deep explanations.

- Identifies decisive factors (things that actually change outcomes)
- Explains the *why* and *how*, not just *what*
- Uses concrete examples so you can imagine real scenarios
- Marks what's fact vs. assumption vs. unknown
- Tells you *when* the advice stops working
- Gives you a minimal way to verify quickly

**Use it when:** Goal is clear but you don't understand the domain, need to evaluate viability, or make business decisions.

[Read the skill →](skills/causal-factor-analysis-codex.md)

---

## Why Two Skills

**Different jobs, different triggers.**

| Intent Clarification | Causal Factor Analysis |
|---------------------|------------------------|
| Trigger: Vague or ambiguous input | Trigger: Clear goal but unfamiliar domain |
| Output: Confirmed provisional goal | Output: Deep causal breakdown + validation plan |
| Depth: Just enough to get direction right | Depth: Full explanation of decisive factors |

Combining them made each half-baked. Separating lets each do its job properly.

---

## How They Work Together

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

## Installation

### Codex
Copy `skills/intent-clarification-codex.md` and `skills/causal-factor-analysis-codex.md` to your Codex skills folder.

### Harness (Desktop)
Copy files to `C:\Users\<YourUsername>\.dsh\skills\`, directory format:

```
C:\Users\<YourUsername>\.dsh\skills\
├── intent-clarification\
│   └── SKILL.md
└── causal-factor-analysis\
    └── SKILL.md
```

Once installed, AI will automatically load the corresponding skill based on your input. You can also manually invoke:
```
skill("intent-clarification")
skill("causal-factor-analysis")
```

See [Harness Integration Guide](docs/harness-integration.md) for details.

---

## What Makes This Different

**vs. Just Asking Follow-up Questions**  
Most AI just asks more questions. These skills *show you* how AI is interpreting your words, so you can correct misunderstandings early.

**vs. Standard Task Breakdown**  
Standard breakdown gives you steps. This gives you *causality*: why each factor matters, how it affects outcomes, when it stops mattering.

**vs. Existing Tools (Rasa, PMAgent, TypeChat, etc.)**  
Researched 6+ projects. None do the complete flow:
- **Rasa:** Has candidate ranking + confidence, but doesn't let you choose
- **PMAgent:** Has option-style questioning, closest match, but only for PM scenarios
- **TypeChat:** Has structured confirmation, but no probability ranking
- **UAP:** Has uncertainty sampling, but doesn't present candidates to users

[See full comparison →](docs/comparison.md)

**Our combination:** Candidate ranking (Rasa) + User choice + Causal explanation + Provisional goals + Reversal conditions

---

## Real Testing

**Stock Investment:** "I want to learn how to buy stocks from scratch" → Listed 4 interpretations → Confirmed user wants to learn *and* actually buy → Broke down market selection/risk tolerance/account setup → One conversation from vague idea to clear path (9.0/10)

**Agent Configuration:** "I'm seeing agent tutorials everywhere, feeling like I need to standardize my usage" → Listed 4 possibilities → Deep dive into agent mechanics/work folder design/handoff skills → User went from "completely don't understand" to full understanding (9.66/10)

[See full examples →](examples/)

---

## More

**Design Philosophy:** From real conversations, not theory. Every principle came from real problems encountered. [Read the full design story →](docs/design-rationale.md)

**Roadmap:** Current v1.0 (intent clarification + causal breakdown + fact/assumption distinction) → v1.1 (understanding check + dynamic priority) → v2.0 (visual causal graphs + drift pattern library)

**Contributing:** Found a case where the skills failed? Have a better example? Issues and PRs welcome.

**License:** MIT - use it however you want.

---

**GitHub:** https://github.com/xiaobai66-web/ai-intent-skills
