# Causal Factor Analysis

When goals are clear, decompose "what factors determine success/failure" and explain the underlying causality.

## Description

After user confirms wanting to "make money with AI cross-border e-commerce services", AI's common problems:
- ❌ Only gives conclusions: "Service-oriented direction ranks first"
- ❌ Doesn't explain why: user doesn't know why to choose this
- ❌ Doesn't state failure conditions: user doesn't know when this judgment breaks down
- ❌ No concrete examples: user can't imagine actual scenarios
- ❌ Doesn't distinguish facts from speculation: treats AI assumptions as market facts

**This skill does:**
1. Identify **decisive factors** (variables that significantly change outcomes)
2. Deeply decompose each factor's **causal chain** (not just "market demand affects revenue", but "how demand step-by-step affects revenue")
3. Use **concrete examples** to aid understanding (not decoration, but scenario imagination)
4. Label **facts/speculation/unknowns** (clarify what's known vs assumed)
5. State **reversal conditions** (when this judgment would change)

## Core Principle

> **Not all details need equal depth, but all "factors that could change decision outcomes" must be identified and explained.**

## When to Use

**Trigger priority**:
- Goal is clear but user unfamiliar with the domain
- User needs to evaluate "is this direction viable"
- Involves business decisions, ROI analysis, risk assessment
- User explicitly asks "explain why"

**Don't trigger**:
- Simple clear goals not needing deep analysis (e.g., "write a function")
- User already familiar with domain, only needs execution
- Pure factual queries (e.g., "how to read files in Python")

## Workflow

### Pre-input (from intent-clarification)

```
Provisional Goal: 【confirmed goal】
Known Facts: 【user explicitly stated】
Info to Confirm: 【still need to ask】
AI Assumptions: 【reasonable inference but unconfirmed】
```

### Step 1: Identify Decisive Factors

From the goal, find **all variables that significantly change outcomes**.

**Criteria**:
- If this factor changes, will the final choice change?
- If this factor fails, can the goal still be achieved?
- Does this factor's state affect investment, risk, return, time, or difficulty?

**Example** (Goal: make money with AI cross-border e-commerce services):
- ✅ Market demand: determines if anyone buys
- ✅ Why customers don't DIY: determines willingness to pay
- ✅ Customer acquisition channels: determines if you can reach customers
- ✅ Delivery capability: determines if you can consistently deliver
- ✅ Cost structure: determines if you profit after costs
- ❌ Website color: not decisive (unless it's a design service)

### Step 2: Deeply Decompose Each Factor

Each decisive factor follows this structure:

```markdown
## 【Factor Name】

### What It Is
Brief definition, one clear sentence.

### Why It Matters
What result or decision this factor affects.

### How It Impacts (Causal Chain) ⭐ Core
Detailed explanation of the **mechanism** by which this factor affects the goal.

Can't just say "market demand affects revenue", must say:
- Where does demand come from (what people face what problems)
- Why they need to solve this problem
- Why they don't solve it themselves
- Under what conditions they're willing to pay
- What result they get after paying
- How this result improves their business
- How this ultimately affects your revenue

### Concrete Example
A realistic hypothetical scenario to aid understanding.

Format:
> Suppose 【specific role】, is 【specific scenario】.  
> You can 【provide what】.  
> They pay not for 【surface product】, but for 【actual result】.

Label: This is a hypothetical example, not a verified success case.

### When Valid / When Invalid
State the boundary conditions of this factor.

✅ Valid conditions: when this factor takes effect
❌ Invalid conditions: when this factor no longer matters

### Current State
Clearly distinguish known, unknown, assumptions.

- ✅ Known: 【confirmed information】
- ❓ Unknown: 【what's still missing】
- ⚠️ Assumption: 【AI's reasonable inference, but unverified】

### Reversal Conditions
What evidence would change the current judgment.

Examples:
- If 20 seller interviews all say "we can do it ourselves", then "market demand" judgment reverses
- If 10 trial orders with no one willing to pay, then "willingness to pay" judgment reverses

### Minimal Validation Plan
Lowest-cost method to verify this factor.

Format:
1. Validation action: what to do
2. Observation metrics: what data to watch
3. Judgment criteria: how much counts as valid
4. Cost estimate: time/money needed
```

### Step 3: Factor Relationship Analysis

Map influence relationships between factors:

```
Market demand → Willingness to pay
      ↓
Customer acquisition → Acquisition cost → Profit margin
      ↓
Delivery difficulty → Rework rate → Actual revenue
```

Label:
- Which factors are **preconditions** (must be met first)
- Which factors are **enhancers** (better to have, but can do without)
- Which factors **influence each other**

### Step 4: Comprehensive Judgment

Based on all factor analysis, provide:

1. **Tentative conclusion**: currently most reasonable direction
2. **Confidence**: high/medium/low (based on known information completeness)
3. **Key assumptions**: which unverified assumptions this conclusion depends on
4. **Next validation steps**: which 2-3 factors to verify first

## Guardrails

1. **Don't over-decompose**: only decompose "decisive factors", not all details
2. **Must have examples**: every factor needs concrete scenarios
3. **Must label state**: clearly distinguish known/unknown/assumptions
4. **Must state reversal conditions**: when judgment would change
5. **Don't fabricate data**: say "needs verification" when lacking real data
6. **Don't promise outcomes**: say "might", not "will"

## Full Example: AI Cross-border E-commerce Service

### Pre-input

```
Provisional Goal: Use AI to help cross-border sellers with product images/videos/localization services, verify if revenue possible

Known Facts:
- User wants to make money
- User's freelance job search unsuccessful
- User unfamiliar with e-commerce
- User wants to see what's profitable before learning

Info to Confirm:
- User's current AI capability level
- Available time investment
- Risk tolerance

AI Assumptions:
- User better suited for service entry vs. self-operated retail
- User needs quick validation vs. long-term learning
```

### Decisive Factor Identification

1. Market demand (is there anyone buying)
2. Willingness to pay (willing to pay or not)
3. Why customers don't DIY (why buy from you)
4. Customer acquisition channels (how to find customers)
5. Delivery capability (can consistently deliver or not)
6. Cost structure (profitable after costs or not)
7. Repeat purchase possibility (one-time or recurring business)
8. Competition (have others already driven prices down)

### Factor 1: Market Demand

**What It Is**  
Whether cross-border sellers truly need AI product image/video/localization services.

**Why It Matters**  
If no demand exists, all subsequent efforts are wasted.

**How It Impacts (Causal Chain)**  
```
Sellers must continuously list new products
   ↓
Each product needs main image, scene images, ad materials
   ↓
Different countries/platforms need different versions
   ↓
Manual work is slow and expensive, AI can accelerate
   ↓
If AI material quality qualifies, sellers willing to outsource
   ↓
You can receive orders and gain revenue
```

But also consider:
- Demand intensity: "must have" or "better to have"
- Demand frequency: one-time or continuous need
- Demand scale: how many times per month does one seller need

**Concrete Example**  
> Suppose a Fujian seller is selling storage boxes to the US and Europe.  
> Weekly launches 10 SKUs, each needs 5 product images + 3 short videos + English/German/French product pages.  
> Manual work takes 2 days per product, costs 500 yuan; you use AI to do one product in 2 hours, quote 200 yuan.  
> They pay not for "AI-generated images", but to save 1.5 days and 300 yuan costs, and get directly listable materials.

**When Valid / When Invalid**  

✅ **Valid conditions**:
- Seller has many products, lists frequently
- Seller lacks dedicated designer
- Seller needs multi-language/multi-platform versions
- Seller wants to quickly test ads

❌ **Invalid conditions**:
- Seller only has few products, rarely updates
- Seller already has design team
- Seller's Canva templates suffice
- Seller requires extremely high material quality (needs photo studio)

**Current State**  
- ✅ **Known**: Cross-border e-commerce market is large, sellers need materials
- ❓ **Unknown**: Small/medium seller actual outsourcing ratio, willingness to pay, acceptable pricing
- ⚠️ **Assumption**: Small/medium sellers prefer outsourcing over learning AI tools themselves

**Reversal Conditions**  
- If interviewing 20 small/medium sellers, <3 express clear needs → market demand judgment reverses
- If AI-generated image quality generally fails commercial standards → technical feasibility fails
- If sellers universally use free AI tools themselves → outsourcing demand fails

**Minimal Validation Plan**  
1. **Validation action**:
   - Find 20 small/medium cross-border sellers (apparel/home/beauty categories)
   - Ask: material creation in-house or outsourced? What pain points?
   - Create 2-3 real product samples
   - Quote and attempt paid trial orders

2. **Observation metrics**:
   - How many state clear pain points
   - How many show interest in samples
   - How many willing to pay for trial order

3. **Judgment criteria**:
   - ≥5 clearly express needs → demand exists
   - ≥2 willing to pay for trial → willingness to pay valid
   - ≥1 repeat purchase or referral → direction viable

4. **Cost estimate**: 1-2 weeks, nearly zero cost

---

### Factor 2: Why Customers Don't DIY

**What It Is**  
Sellers can use AI to create materials themselves, why pay you?

**Why It Matters**  
If customers can easily solve it themselves, they won't keep paying.

**How It Impacts (Causal Chain)**  
```
AI tools already widespread
   ↓
Sellers can also use Midjourney/Stable Diffusion
   ↓
But:
   - Don't know how to handle lighting, composition, product proportions
   - Unfamiliar with target country visual habits
   - Batch processing 30 SKUs very troublesome
   - Need repeated revisions, unified style, platform size adaptation
   - Boss doing images means no time for product selection and ads
   ↓
Outsourcing to you saves time and trial-and-error costs
   ↓
If your delivery quality stable, communication cost low, rework rare
   ↓
Customers willing to keep paying
```

**Concrete Example**  
> Seller Lao Wang knows Midjourney, but making one image takes 20 prompt iterations, generates 50 images to pick 1.  
> After image done still needs cutout, size adjustment, text adding, half a day per product.  
> He has 100 products to list, if DIY takes 50 days; outsource to you 10 days done, he saves 40 days for selection and ads.  
> You charge 200 yuan/product, he thinks it's worth it because his time is worth more.

**When Valid / When Invalid**  

✅ **Valid conditions**:
- Seller doesn't know or isn't proficient with AI tools
- Seller has many products, batch processing cost high
- Seller's time more valuable (selection/ads/customer service)
- Seller requires unified style and professionalism

❌ **Invalid conditions**:
- Seller is designer themselves
- Seller team has dedicated material person
- AI tools become extremely easy (one-click commercial-grade materials)
- Your delivery quality worse than seller DIY

**Current State**  
- ✅ **Known**: AI tools indeed spreading
- ❓ **Unknown**: Small/medium seller actual AI usage ability, time cost, outsourcing willingness
- ⚠️ **Assumption**: Most small/medium sellers unwilling to spend time learning and batch processing

**Reversal Conditions**  
- If sellers universally say "we can do it ourselves" → outsourcing demand fails
- If AI tools launch "one-click product image generation" → your value decreases
- If your delivery quality unstable, much rework → customers prefer DIY

**Minimal Validation Plan**  
1. **Validation action**:
   - During trial order process ask: how do you currently create materials?
   - Observe: is seller already using AI tools?
   - Compare: your delivery vs seller DIY results

2. **Observation metrics**:
   - Seller's current material quality
   - How long seller takes to DIY one product
   - Whether seller expresses "too troublesome"

3. **Judgment criteria**:
   - If seller DIY one product >4 hours → outsourcing has value
   - If your delivery quality > seller DIY → professional advantage valid
   - If seller says "saved a lot of time" → payment reason valid

4. **Cost estimate**: included in trial validation, no extra cost

---

(Other factors follow same structure: customer acquisition channels, delivery capability, cost structure, repeat purchase possibility, competition)

---

### Comprehensive Judgment

**Tentative Conclusion**  
AI cross-border e-commerce service is a direction **worth validating**, reasons:
1. Market demand possibly exists (small/medium seller material creation pain point)
2. Outsourcing value possibly valid (batch processing, time savings)
3. Low startup cost (no inventory, ads, system building needed)
4. Fast validation (1-2 weeks for initial results)

**Confidence**: Medium (60-70%)  
- Theoretical logic reasonable, but lacks actual market validation
- Most judgments based on reasonable inference, not confirmed facts

**Key Assumptions** (need verification)  
1. Small/medium sellers indeed have continuous material creation needs
2. Sellers willing to pay for outsourcing services
3. AI-generated material quality can meet commercial standards
4. You can consistently deliver and control rework rate

**Next Priority Validation**  
1. **Market demand** (most critical): interview 20 sellers, create 2-3 samples, attempt paid trial
2. **Delivery capability**: actually create 2-3 complete product material sets, test quality and time
3. **Willingness to pay**: quote and observe conversion rate

**Not Recommended Priority**  
- ❌ Don't spend months first "learning complete cross-border e-commerce knowledge"
- ❌ Don't develop complex automation tools first
- ❌ Don't become seller yourself first (startup cost too high)

## Handoff from Previous Skill

```
intent-clarification output:
  provisional goal + known/unknown/assumptions
    ↓
causal-factor-analysis input:
  start identifying decisive factors
    ↓
causal-factor-analysis output:
  deep decomposition of each factor + validation plans
    ↓
(optional) task-map-generation:
  generate visual task map
```

## MVP Boundaries

**Included**:
- ✅ Decisive factor identification
- ✅ Causal chain deep decomposition (what/why/how impacts)
- ✅ Concrete examples
- ✅ Valid/invalid conditions
- ✅ Facts/speculation/unknowns labeling
- ✅ Reversal conditions
- ✅ Minimal validation plans

**Not yet included** (for future versions):
- ❌ Automatic market data scraping
- ❌ Complex factor weight calculation
- ❌ Visual causal graph
- ❌ Auto-generated validation questionnaires

## FAQ

**Q: Must all factors be this detailed?**  
A: No. Only "decisive factors" (that change final decisions) need deep decomposition. Secondary details just mention briefly.

**Q: What if there are 10 decisive factors?**  
A: First decompose the most critical 3-5. Others can be briefly stated, expanded when needed.

**Q: Must examples be real cases?**  
A: No. Can be reasonable hypothetical scenarios, but must label "this is a hypothetical example, not a verified success case".

**Q: What if user doesn't need such detailed analysis?**  
A: User can interrupt or request simplification anytime. This skill mainly for "user unfamiliar with domain, needs deep understanding of causality" scenarios.
