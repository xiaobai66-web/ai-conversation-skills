# Intent Clarification

Clarify what the user actually wants before answering or executing.

## Description

When a user says "I want to buy stocks," AI might interpret it as:
- Teach me how to buy (learning)
- Recommend stocks (execution)
- Judge timing (consultation)
- Help me open an account (operation)
- Analyze if this idea makes sense (validation)

**If AI guesses wrong, the entire conversation goes off track.**

This skill:
1. **Doesn't rush to answer**, analyzes possible interpretations first
2. **Lists candidate intents** (2-4), showing the user how AI understands them
3. **Asks one key question** to quickly confirm direction
4. **Forms a provisional goal**, clearly distinguishing facts, assumptions, and unknowns

## When to Use

**Trigger priority** (complex, high-risk scenarios):
- Vague goals: `I want to.*|I'm thinking about.*|trying to figure out.*`
- Needs decomposition: `don't know how.*|not sure where.*|need help analyzing.*`
- Multiple interpretations: same input has 3+ reasonable interpretations
- High-risk decisions: involves money, legal, health, career, business, long-term commitment
- Cross-domain: user explicitly states "I'm completely unfamiliar with this"

**Don't trigger** (simple, clear scenarios):
- Simple factual questions: "What time is it?" "How to read a file in Python?"
- Clear execution requests: "Write a function for me" "Fix this bug"
- Chat or feedback: "OK" "Continue" "Nice"

**Gray area** (context-dependent):
- "I want to learn Python": beginner → trigger; has other language background → simplify
- "Help me evaluate this business idea": trigger (needs goal clarification)
- "How to do this project": complex project → trigger; small feature → don't trigger

## Workflow

### Step 1: Receive user input, silent analysis

After user input, **don't answer immediately**, analyze internally:
1. What is this sentence doing? (asking/seeking judgment/seeking support/proposing action/expressing idea)
2. What might the user want? (knowledge/advice/plan/concrete execution)
3. What background might have led to this? (encountered problem/wants change/saw opportunity/casual interest)
4. Where will different interpretations take the task?

### Step 2: Generate candidate intents (2-4)

**Principles**:
- List interpretations that **actually change the subsequent answer**
- Don't list "all possibilities" (infinitely many, makes it harder to choose)
- Keep a "none of these, what I mean is…" option

**Format**:

```
You said "【user's words】", I see a few possibilities:

| Candidate | Current Evidence | Tentative Confidence |
|---|---|---|
| A. 【interpretation 1】 | 【evidence from original words】 | High |
| B. 【interpretation 2】 | 【inferred from context】 | Medium |
| C. 【interpretation 3】 | 【common in domain, but no user evidence】 | Low |

At the same time, the following information affects the answer but is currently unclear:
- 【missing info 1】
- 【missing info 2】
- 【missing info 3】
```

**Confidence standards**:
- **High**: directly supported by user's words
- **Medium**: some evidence, but other interpretations exist
- **Low**: only common possibility in domain, no user evidence currently

**Important**: Probability ranking ≠ clarification priority

```
Clarification priority ≈ probability × impact if wrong × irreversibility
```

A low-probability but high-loss-if-wrong branch should be clarified first.

### Step 3: Identify key divergence, ask only one question

Find the **question that best distinguishes different paths**.

❌ Don't ask:
- "What exactly do you want to do?" (too broad)
- "What's your budget?" (too early for details)

✅ Ask:
- "Are you closer to 【learning】 or 【execution】?"
- "Do you already have specific targets, or need help screening?"

### Step 4: User confirmation

User can:
- Choose one option (e.g., "A")
- Combine multiple (e.g., "A+B")
- Reject all, clarify true intent

### Step 5: Form provisional goal

Based on confirmation, generate:

```
Provisional Goal: 【task description after user confirmation】

Basis:
✅ User explicitly said: 【facts】
❓ Still need to confirm: 【info to ask】
⚠️ AI temporarily assumes: 【reasonable inference, but unconfirmed】
```

**Key principles**:
- Use "provisional goal" not "final goal", allowing subsequent correction
- Distinguish **facts, assumptions, unknowns**
- Interpretations rejected by user must not continue as goals

## Guardrails

1. **Don't guess psychology**: analyze possible goals, don't do psychological diagnosis
2. **Don't execute directly**: even if one interpretation is 90% probable, confirm first
3. **Only ask at divergence points**: if different interpretations can be answered the same way, don't ask
4. **Explicit confirmation for high-risk**: irreversible operations require double confirmation
5. **Mark inferences**: AI's inferences must be labeled "temporary assumption"

## Full Example: Stock Scenario

### User Input
> I want to learn how to buy stocks from scratch.

### AI Internal Analysis (not shown to user)
- This sentence is: asking (learning type)
- Might want: knowledge / knowledge+actual operation
- Background: might want to make money, saw others trading, casual interest
- Different interpretations: pure learning vs learn then buy vs want recommendations

### AI Output (shown to user)

You said "learn how to buy stocks from scratch", I see a few possibilities:

| Candidate | Current Evidence | Tentative Confidence |
|---|---|---|
| A. Want to first understand stocks, accounts, orders, and basic risks | "from scratch learn" | High |
| B. Want to complete first actual purchase after learning | "how to buy" implies practical operation | Medium |
| C. Want to know how to pick first stock or ETF | buying stocks usually involves target selection | Medium-low |
| D. Want direct specific stock recommendations | no mention of targets or recommendations currently | Low |

At the same time, the following information affects the answer but is currently unclear:
- Your country or market
- Whether you already have a securities account
- Learning first, or actually buying soon
- Acceptable capital and risk
- Plan to hold for days, months, or years

**What I most want to confirm**: when you say "learn how to buy", which is closer?
- **A. First understand knowledge and process, not buying yet**
- **B. Hope to complete one actual purchase after understanding**
- **C. Both, learn first then practice**

### User Confirmation
> B, after understanding I want to actually try buying once.

### AI Forms Provisional Goal

```
Provisional Goal: Learn basic knowledge and process of stock purchase, and complete one small actual purchase

Basis:
✅ User explicitly said:
  - Starting from scratch
  - Want to actually buy once after learning

❓ Still need to confirm:
  - Country/market location
  - Whether already has securities account
  - Investable capital range
  - Risk tolerance

⚠️ AI temporarily assumes:
  - User hopes for small trial-and-error not large investment
  - Better to start with index funds/ETFs rather than individual stocks
  (These assumptions need verification in subsequent steps)
```

→ Now can hand off to `causal-factor-analysis` to continue decomposing key factors.

## Handoff to Next Skill

```
intent-clarification output:
  provisional goal + known facts + info to confirm + AI assumptions
    ↓
causal-factor-analysis input:
  start decomposing "what factors determine success/failure for this goal"
```

## MVP Boundaries

**Included**:
- ✅ Candidate intent enumeration (2-4)
- ✅ Evidence and confidence labeling
- ✅ Key divergence identification (ask only one question)
- ✅ Provisional goal generation
- ✅ Facts/assumptions/unknowns distinction

**Not yet included** (for future versions):
- ❌ Automatic GitHub project scanning
- ❌ Complex multi-round understanding scoring
- ❌ Visual intent tree
- ❌ Auto-generated interview questionnaires

## FAQ

**Q: Must we go through this process every time?**  
A: No. Simple clear requests don't trigger. Only when "one sentence has multiple interpretations and choosing wrong affects subsequent steps" does it trigger.

**Q: What if user says "whatever, you decide"?**  
A: Indicates current candidates may all be wrong, or user hasn't thought it through. Don't decide for user, instead help clarify "what matters most to you".

**Q: What if user chooses multiple options (A+B)?**  
A: Combinations allowed, forming a new provisional goal. For example "both learning and actual operation" is a reasonable combined goal.

**Q: What if provisional goal turns out to be misunderstood later?**  
A: User can correct anytime. Precisely because it's labeled "provisional", subsequent correction is allowed. The key is letting user see what the current understanding is.
