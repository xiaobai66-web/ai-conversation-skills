# AI Intent Skills

**Two skills that help AI understand what users actually want before acting.**

Stop AI from guessing wrong and wasting your time.

---

## The Problem

You say **"I want to buy stocks"**

AI might think you mean:
- Teach me the basics (learning)
- Recommend specific stocks (execution)
- Help me open an account (setup)
- Judge if now is a good time (consultation)
- Analyze if this idea makes sense (validation)

**If AI picks wrong, the whole conversation goes sideways.**

You say **"I want to do AI e-commerce"**

AI might give you a plan immediately, but:
- Doesn't explain *why* certain directions work
- Doesn't tell you *when* the advice breaks down
- Doesn't distinguish facts from guesses
- Doesn't show you how to verify quickly

**You end up learning for months without knowing if it's even viable.**

---

## The Solution

Two separate skills that work together:

### 1. Intent Clarification
**What it does:** Figures out what you actually want before answering.

- Lists 2-4 possible interpretations of your words
- Shows you the evidence for each
- Asks *one* key question to confirm direction
- Forms a "provisional goal" you can correct anytime

**Use it when:** Your request is vague, has multiple meanings, or involves high-risk decisions.

[Read the skill →](skills/intent-clarification-harness.md)

### 2. Causal Factor Analysis
**What it does:** Breaks down "what determines success" with deep explanations.

- Identifies decisive factors (things that actually change outcomes)
- Explains the *why* and *how*, not just *what*
- Uses concrete examples so you can imagine real scenarios
- Marks what's fact vs. assumption vs. unknown
- Tells you *when* the advice stops working
- Gives you a minimal way to verify quickly

**Use it when:** Goal is clear but you don't understand the domain, need to evaluate viability, or make business decisions.

[Read the skill →](skills/causal-factor-analysis-harness.md)

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

## Real Examples

### Stock Investment
- **Input:** "I want to learn how to buy stocks from scratch"
- **Intent Clarification:** Listed 4 interpretations, confirmed user wants to learn *and* actually buy
- **Causal Factor Analysis:** Broke down market selection, risk tolerance, account setup with full causality
- **Outcome:** User went from vague idea to clear path in one conversation
- **Score:** 9.0/10 (some drift during explanation phase)

### Agent Configuration
- **Input:** "I'm seeing agent tutorials everywhere, feeling like I need to standardize my usage"
- **Intent Clarification:** Listed 4 possibilities (learn methods, fix pain points, build system, evaluate ROI)
- **Causal Factor Analysis:** Deep dive into agent mechanics, work folder design, handoff skills, maintenance cost
- **Outcome:** User went from "completely don't understand" to full understanding in one conversation
- **Score:** 9.66/10

[See full examples →](examples/)

---

## Installation

### For Codex Users

Copy `skills/intent-clarification-codex.md` and `skills/causal-factor-analysis-codex.md` to your Codex skills folder.

Format: YAML frontmatter + markdown

---

### For Harness Users

#### Desktop Harness (Recommended)

1. **Create skill directory structure:**

```bash
C:\Users\<YourUsername>\.dsh\skills\
├── intent-clarification\
│   └── SKILL.md
└── causal-factor-analysis\
    └── SKILL.md
```

2. **Copy files:**
   - Copy `skills/intent-clarification-codex.md` → `C:\Users\<YourUsername>\.dsh\skills\intent-clarification\SKILL.md`
   - Copy `skills/causal-factor-analysis-codex.md` → `C:\Users\<YourUsername>\.dsh\skills\causal-factor-analysis\SKILL.md`

3. **Verify:**
   - In a new Harness conversation, the system prompt should include an `<available_skills>` list
   - Both skill names should appear → installation successful

**Note:** Desktop version requires **directory format** (`skill-name/SKILL.md`), not single `.md` files.

#### Web Harness (Source Development)

Copy `skills/intent-clarification-harness.md` and `skills/causal-factor-analysis-harness.md` to your Harness source code `skills/` directory.

Format: markdown heading (no YAML frontmatter)

---

### How to Use

Once installed, when you say something matching the trigger conditions (e.g., "I want to make a task management skill"), AI will automatically load the corresponding skill.

You can also manually invoke:
```
skill("intent-clarification")
skill("causal-factor-analysis")
```

---

## Why Two Skills Instead of One?

**Different jobs, different triggers:**

**Intent Clarification:**
- Triggers: User says something vague or ambiguous
- Output: Confirmed provisional goal
- Depth: Just enough to get direction right

**Causal Factor Analysis:**
- Triggers: Goal is clear but user doesn't understand the domain
- Output: Deep causal breakdown + verification plan
- Depth: Full explanation of decisive factors

Combining them made each half-baked. Separating lets each do its job properly.

---

## What Makes This Different

### vs. Just Asking Follow-up Questions
Most AI just asks more questions. These skills *show you* how AI is interpreting your words, so you can correct misunderstandings early.

### vs. Standard Task Breakdown
Standard breakdown gives you steps. This gives you *causality*: why each factor matters, how it affects outcomes, when it stops mattering.

### vs. GitHub Projects (Rasa, PMAgent, TypeChat, etc.)
We researched 6+ projects. None do the complete flow:
- **Rasa:** Has candidate ranking + confidence, but doesn't let you choose
- **PMAgent:** Has option-style questioning, closest match, but only for PM scenarios
- **TypeChat:** Has structured confirmation, but no probability ranking
- **UAP:** Has uncertainty sampling, but doesn't present candidates to users

[See full comparison →](docs/comparison.md)

**Our combination:**
- Candidate ranking (from Rasa)
- User choice (our innovation)
- Causal explanation (our innovation)
- Provisional goals (our innovation)
- Reversal conditions (our innovation)

---

## Design Philosophy

**From real conversations, not theory.**

These skills came from 10 days of actual back-and-forth with Codex (Sept 30 - Oct 9, 2026), working through:
- Stock investment scenario (revealed drift issues)
- Agent configuration scenario (proved the approach works)
- E-commerce direction evaluation (tested causal analysis depth)

Every principle came from real problems we hit.

[Read the full design story →](docs/design-rationale.md)

---

## Roadmap

**Current: MVP (v1.0)**
- ✅ Intent clarification with 2-4 candidates
- ✅ Causal factor deep decomposition
- ✅ Facts/assumptions/unknowns distinction
- ✅ Reversal conditions
- ✅ Minimal validation plans

**Next: Enhancements (v1.1-1.2)**
- [ ] Understanding check mechanism (ask user to rephrase)
- [ ] Dynamic factor priority adjustment
- [ ] Automatic GitHub precedent search
- [ ] Richer examples library

**Future: Polish (v2.0+)**
- [ ] Visual causal graphs
- [ ] Real usage data collection
- [ ] Common drift pattern library
- [ ] Multi-language support optimization

---

## Contributing

Found a case where the skills failed? Have a better example? Want to add trigger patterns?

Issues and PRs welcome. Please include:
- The actual user input
- What went wrong or could improve
- Your suggested fix

---

## License

MIT License - use it however you want.

---

## Citation

If you use these skills in your research or product:

```
@software{ai_intent_skills_2026,
  author = {xiaobai66-web},
  title = {AI Intent Skills: Intent Clarification and Causal Factor Analysis},
  year = {2026},
  url = {https://github.com/xiaobai66-web/ai-intent-skills}
}
```

---

## Credits

Built through iterative conversation with Codex, based on real pain points encountered in:
- Stock investment exploration
- Agent configuration design
- E-commerce direction validation
- Business model evaluation

Special thanks to the open-source projects we studied:
- Rasa (candidate ranking approach)
- PMAgent (option-style questioning)
- TypeChat (structured confirmation)
- UAP (uncertainty sampling)
