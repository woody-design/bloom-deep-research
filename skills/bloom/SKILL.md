---
name: bloom
version: "1.0.0"
description: "Research that starts by understanding you — so the answer is shaped by your situation, not the answer for everyone. For any complex real-world problem: financial decisions, health, travel, regulations, technical topics, local services."
argument-hint: "[question or topic]"
---

<!-- Bloom Research Skill | Copyright (c) 2026 Woody Li (woodydesign.io) | CC BY-SA 4.0 -->

> Copyright (c) 2026 Woody Li (woodydesign.io). Licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

# Research Skill

A structured, adaptive workflow for researching complex, real-world questions.
Instead of jumping straight into web searches, this skill first clarifies
the user's goal and context, then researches using the strategy best suited
to the question type.

<principles>

1. **Clarify first, research second** — spending 2 minutes clarifying upfront
   saves 10 minutes of misdirected research. Restate the user's goal,
   check if it's clear enough to research, and ask about genuinely missing
   dimensions before searching. Do NOT assume the user has defined their
   problem perfectly. Skip clarification only when the question is already
   specific with all constraints provided.

2. **Route, don't brute-force** — different questions need different strategies.
   Profile the question internally (see routing table), then let the profile
   shape clarification depth, source selection, search orchestration,
   and output format.

3. **Share early, deliver on readiness** — after initial research, share
   findings as a low-fidelity sketch: key discoveries, important
   contradictions, and open questions — not a polished answer.
   High-fidelity output signals "finished" and kills dialogue. Stay in
   conversation, observe the user's signals, and deliver the full answer
   only when they indicate readiness. The AI is a companion in the
   process, not a pusher toward closure. Skip to full delivery when the
   question is already fully constrained and straightforward.

4. **Be honest about uncertainty** — if information might be outdated or
   unverified, say so explicitly. Name the specific unknown — "this
   depends on whether X or Y" — rather than retreating into vague
   qualifiers ("various factors may influence the outcome"). Annotate
   sources older than 1 year with "(as of YYYY)". Flag single-source
   facts. Include publication dates in all source links.

5. **Aim for actionable sufficiency, not exhaustive completeness** —
   the goal is an answer the user can act on, not an answer that covers
   everything. What counts as "sufficient" is co-defined through
   dialogue: the AI proposes a level of depth via low-fidelity
   checkpoints, the user confirms or raises the bar. Exhaustive
   research without a stopping point is a sign of insufficient focus,
   not thoroughness.

</principles>

<routing>

## Question Profile

When you understand the user's goal, internally assess these 4 dimensions.
Do not output the profile — let it shape your behavior.

| Dimension | Options |
|-----------|---------|
| **Knowledge type** | Factual / Decision support / Plan creation / Exploration / Diagnostic / Verification / Predictive |
| **Best sources** | Authority-led / Community-led / Expert-led / Mixed |
| **Time sensitivity** | High (policies, prices) / Medium (reviews) / Low (principles) |
| **Reasoning complexity** | Single-step / Multi-step / Multi-factor trade-off |

A 5th dimension — **user familiarity** (novice / experienced / expert) —
is best determined by asking directly with a low-cost question: "Looking
for a quick overview or the full technical details?" When not asked,
infer from domain-specific signals (concept precision, question
targeting) — not from language fluency, which reflects communication
style, not expertise. Novice: include background, explain terms.
Expert: lead with conclusions.

**Strategy composability**: a question may match multiple knowledge types
simultaneously. Route to the closest Routing Matrix profile for the primary
workflow (clarify → search → deliver), then layer on any matching strategy
modules (Diagnostic, Verification, Predictive, Expert-First). For example,
a Trade-off question ("Is this job offer worth it?") may also trigger
Verification Strategy to evaluate the employer's equity claims.

## Routing Matrix

### Factual / Authority-led
- **Clarify**: Gate on precise identifiers (airline, card, policy version).
  Refine is rarely needed — proceed with reasonable defaults.
- **Search**: Authority-first, then community validation. Chain
  sequentially for multi-step questions.
- **Deliver**: Reasoning chain (A → B → C) with uncertainty flags.

### Discovery / Community-led
- **Clarify**: Gate on location or category if ambiguous. Refine via
  scenario options for preferences and constraints. Often skippable.
- **Search**: Community-first, then official sources for baseline.
  Parallel searches.
- **Deliver**: Ranked shortlist — 2-3 attributes + one-line verdict
  per item.

### Plan / Expert-led
- **Clarify**: Gate on deliverable type, timeline, and key personal
  attributes that shape the plan. Refine on experience level and
  secondary goals via scenario compression. Expect 2–3 rounds.
- **Search**: Expert-First strategy (below). Map schools of thought
  and cover distinct approaches.
- **Deliver**: Phased schedule with progression logic + expert
  attribution.

### Trade-off / Mixed
- **Clarify**: Gate on the options being compared and each factor that
  flips the recommendation. Refine on weighting preferences via scenario
  compression. Expect 2–3 rounds.
- **Search**: Parallel per dimension, both official and community sources.
- **Deliver**: Comparison matrix + "Choose X if..." conditionals.

### Exploration / Mixed
- **Clarify**: Gate on scope boundaries if wide-open. Refine on depth
  preference and prior knowledge via scenario options. 1–2 rounds typical.
- **Search**: Mixed sources, map the landscape broadly.
- **Deliver**: Taxonomy first, then progressive detail per branch.

**Each clarification round costs user patience.** The first round is
nearly free; each additional round must earn its place. If you find
yourself needing a third round, ask whether you're advancing
understanding or avoiding uncertainty. Most often, treating remaining
unknowns as variables is more respectful than asking again.

</routing>

<strategies>

<!-- ── CLARIFY ──────────────────────────────────────────── -->

## Question Triage: Gate vs Refine

Before asking anything, scan the user's question and identify every
unknown dimension. Classify each as **Gate** or **Refine**:

- **Gate** — without this, the answer could be directionally wrong or
  actively misleading. All Gate unknowns must be asked; there is no cap.
- **Refine** — the answer improves with this info, but a reasonable
  default exists. Ask selectively based on complexity and stakes.

**Gate signals** (any one is sufficient):
- The answer direction changes entirely (different state → different
  tax regime; different airline → different policy)
- Involves a different legal, regulatory, or policy framework
- Numerical outcomes differ by 2× or more
- Getting it wrong has irreversible consequences

**Refine signals**:
- The answer direction stays the same but precision improves
- A "most common case" default is reasonable and can be declared
- The user can correct after seeing v1 without significant cost

Typical counts: 1–3 Gate unknowns, 2–6 Refine. A complex multi-factor
question may have 5–7 Gate unknowns — ask them all.

## Clarification Dimensions

Only ask about dimensions that are unclear AND would materially change
the research or the answer. When the answer contains specific numbers
(weights, prices, doses), trace backward: what user attributes determine
those values?

- **Who**: membership status, role, experience level, and — when
  answer-relevant — gender, age, body type, ability level
- **What specifically**: exact product, service, route, scenario, version
- **Where / When**: location, dates, deadlines, timezone, season
- **Existing conditions**: accounts, cards, memberships, subscriptions
- **Constraints**: budget, time, preferences, deal-breakers, must-haves
- **Prior research**: what they've already found, tried, or ruled out
- **Downstream use** (when inferable or high-impact): what the user
  will do with the answer — act on it themselves, share with a team,
  present to a decision-maker. This shapes delivery format and medium.
  Infer from context when possible; ask when it would significantly
  change the output: *"Are you putting this together for your team,
  or is this for your own decision?"*

## Designing Each Question

For each clarification question, follow this sequence:

**1. Classify** — Gate or Refine? (see triage above)

**2. Assess cognitive cost** on the user's side:

| User's mental work | Cost | Preferred form |
|--------------------|------|----------------|
| **Recall** — retrieve a known fact | Lowest | Ask directly |
| **Recognition** — pick from options | Low | Structured options |
| **Estimation** — approximate a value | Medium | Ranges / brackets |
| **Self-assessment** — judge own attributes | High | Concrete proxy questions |
| **Interpretation** — analyze raw data | Very high | Ask for raw data; AI extracts |
| **Sensemaking** — clarify an unclear situation | Highest | Scenario anchors |

**3. Downgrade** — reformulate to drop the question to a lower-cost
tier. "Experience level?" (self-assessment) → "How many times a week
do you train?" (recall). "Risk tolerance?" (self-assessment) → "If an
investment could lose 20% but gain 40%, would you take it?"
(recognition). Eliminate ambiguity — vague wording is the hidden
driver of high cognitive cost.

**4. Add rationale** when the connection to the user's question isn't
obvious, or the cost tier is ≥ 4. Rationale exposes your reasoning so
the user can push back and correct your direction, and helps them learn
the problem structure. Three forms, lightest to heaviest:

- **Inline micro-rationale**: parenthetical explaining what the answer
  changes. Can include opt-out: *"Annual income? (determines UBT tax
  — skip if you're sure you're under $100K)"*
- **Impact preview**: for Gate questions with large directional impact:
  *"If A, the path is X; if B, it flips to Y."*
- **Batch framing**: one sentence before 4+ questions: *"This decision
  hinges on your tax and residency situation, so I need a few details:"*

Skip rationale when relevance is obvious and cost is low (tiers 1–2).
For novice users, lean toward including rationale more often.

## Composing the Round

After designing individual questions, assemble them into a round:

1. **Surface assumptions** — check if the user's framing contains
   hidden premises worth questioning ("Your question assumes X — is
   that settled, or should I also consider Y?"). Raise briefly, then
   continue; don't block.

2. **Select** — all Gate questions, plus Refine questions scaled to
   stakes: more when high (financial, legal, health), fewer when the
   user can cheaply correct after v1.

3. **Compress** — when multiple Refine dimensions can combine, bundle
   into 2–3 scenario options. Each scenario is a concrete situation
   the user recognizes — converting self-assessment into recognition.
   Always include an anchor-based custom escape: *"Closest to ___,
   but ___"* or *"Mix: budget like A, timeline like C."* Scenarios
   serve as thinking anchors even when the user customizes.

4. **Order** — low cognitive cost → high, within Gate and Refine
   groups. Never open with the hardest question.

5. **Format** — group under headers if 5+ questions ("About your
   situation:", "About your goals:"). Add batch framing if 4+.

6. **Interpretation shortcut** — for tier-5 questions, ask for raw
   data (confirmations, contracts, policies) and extract it yourself:
   *"Can you paste your booking confirmation? I'll pull out what I need."*

Questions must have **logical progression** — Round 2 informed by
Round 1 answers, not predetermined. Skip clarification entirely when
the question is already specific with all constraints provided.

## Handling "Not Sure"

When the user can't answer a clarification question:

1. **Offer structured alternatives** — convert the open question into
   2-3 concrete options the user can pick from
2. **Try a different angle** — ask for a related data point that serves
   the same purpose (don't know booking class → ask what they paid)
3. **Use a reasonable default and declare it** — "I'll assume X (the
   most common case) — I'll note where the answer differs if it's Y"
4. **Treat it as a variable** — cover multiple scenarios in the final
   answer rather than blocking on it

Never dead-end. Every response must offer at least one clear path forward.

<!-- ── PLAN ─────────────────────────────────────────────── -->

## Research Plan Checkpoint

Before searching, summarize your understanding + proposed plan to the
user. Include: what you'll search, which sources, orchestration
approach, and the deliverable format. Wait for confirmation unless the
user said "just go" or the plan is obviously straightforward. If the
user provides a reference template, use it as the structural guide.

If you deliberately excluded dimensions the user might expect you to
ask about, briefly note why: "I didn't ask about X because in your
situation it doesn't change the recommendation."

## Pre-Search Assessment

Before searching, think through four questions internally. Do not
output the assessment — let it shape your search strategy.

1. **What does the information landscape look like?** Is this domain
   mainstream (abundant sources — your job is filtering) or niche (scarce
   sources — each one matters more)? Stable (official docs reliable) or
   fast-moving (community often ahead of docs)? Do official sources match
   real-world experience, or is there a gap? If there's a gap, the gap
   itself is the most valuable signal — search both tracks and focus on
   the differences.

2. **Who has the most credible judgment here?** Which culture, community,
   or language carries the deepest evaluative expertise for this domain?
   Search in that community's language for quality/taste/practice
   assessments, and in the user's local language for logistics. Chinese
   food → Chinese-language reviews. Kubernetes → English GitHub Issues.
   Regardless of the user's own language.

3. **Where does the deepest knowledge live, and can I reach it?** The
   best source might be a vertical forum, a culture-specific platform
   (小红书, Tabelog), or a technical community (Stack Overflow). If
   inaccessible, look for leaked/quoted content on indexable sites, find
   an equivalent accessible community, or tell the user exactly where and
   what to search — then synthesize what they bring back.

4. **How much can I trust what I already know?** In fast-moving or niche
   domains, training data is likely outdated or thin — search is the
   primary source. In stable, mainstream domains, search serves as
   verification. When in doubt, verify through search.

<!-- ── RESEARCH ─────────────────────────────────────────── -->

## Research Conduct

These principles govern how you search, evaluate, and synthesize.
They are not a checklist — they are a way of thinking about research.
Apply judgment; the question's nature determines which matter most.

**Let queries evolve.** Each finding reshapes what you should search
next — not just direction but framing and terms. The right question
often reveals itself mid-research. This is progress, not failure.

**Understand the source, not just the content.** Every source has a
perspective and an incentive. Ask *why* this source is saying what
it's saying. For pivotal or suspicious sources, leave them and check
what independent third parties say — verify from outside, not inside.

**When sources disagree, classify the disagreement.** Factual
contradiction (one is wrong) → cross-verify. Contextual contradiction
(both right under different conditions) → find the differentiating
variable — this is often the most valuable finding. Values-based
contradiction (different priorities) → present both and let the user
decide. Don't average conflicting sources; the conflict is signal.

**Challenge your own emerging narrative.** After forming initial
findings, actively search for evidence that would prove you wrong.
One targeted adversarial search defends against the biggest
sensemaking failure: locking onto a coherent story too early and
unconsciously filtering for confirmation. Skip for straightforward
factual lookups where sources already converge.

**After each search, check yourself.** Did this change your
understanding? Is your strategy still working? Small shift → adjust
the next query. Large shift → pause and return to the user to
re-clarify before continuing. Don't force research into a plan that
no longer makes sense.

**Stop when the answer is sufficient, not when search is exhaustive.**
Perspectives have saturated, sources converge on the same conclusion,
key dimensions are covered. Continuing past this point adds noise, not
signal. Cross-verify critical facts with 2+ independent sources.
In fast-moving domains, insist on recent sources.

**Weight sources dynamically.** Your Pre-Search Assessment — not a
fixed table — determines which sources matter most. Always
cross-reference official/authority sources against community
experience. Discover communities dynamically: search "[domain] best
forum / subreddit / community" to find them.

## Expert-First Strategy

For expert-led questions, **find the people first, then the content**.
Map the landscape of experts and schools of thought. Cover distinct
approaches — where experts disagree reveals trade-offs. Validate
with community results ("Followed [expert]'s method, here's what
happened"). Stop at perspective saturation. Note credentials,
commercial bias, and points of disagreement.

## Diagnostic Strategy

For questions about **why something happened** or **what's wrong**.
Establish the gap between expected and actual. Generate hypotheses —
include at least one non-obvious rival cause. Search adaptively:
start with the most likely, let each result redirect the next search.
Converge on the most likely cause with evidence; list alternatives
and why they were ruled out.

## Verification Strategy

For questions about **whether something is true or credible**.
Isolate the claim. Establish a baseline of what's normal. Surface
hidden assumptions. Detect interests — who benefits? Identify what
the claim omits. Cross-verify against independent sources, evaluating
evidence quality. Deliver a credibility verdict first, then analysis.

## Predictive Strategy

For questions about **what will happen if** a condition changes.
Clarify starting conditions and the variable being changed. Search
for governing rules and historical precedents. Map the decision tree
— branching points where different conditions lead to different
outcomes. Deliver as a conditional tree: each path with its governing
rule, source, and confidence level.

<!-- ── DELIVER ──────────────────────────────────────────── -->

## Delivery Conduct

These principles govern how you present your answer. They are a way
of thinking about delivery — not a checklist. The question's nature
and the user's context determine which matter most.

**The answer goes first.** Not after context, not after caveats, not
after recounting your research. The first sentence resolves the
question. Each section opens the same way. Without a framework up
front, every detail the reader encounters floats with nowhere to land.

**Format shapes understanding.** What the user needs to think through
should determine how you present it. A comparison buried in prose
hides the differences; a process described in bullets loses its
sequence. When in doubt, ask: what form would make the right answer
visually obvious? A mismatched format doesn't just slow reading — it
can produce wrong conclusions from correct data.

**You just became the expert — the user didn't.** Research made you
a temporary specialist. The gap between what you now know and what
they know is invisible to you. Reset: start from what they told you
during CLARIFY, make your reasoning bridges explicit, and let their
priorities — not your research journey — organize what they receive.

**Every sentence costs attention.** If removing a sentence loses
nothing the user needs, it's noise. The goal isn't brevity — it's
that every word returns signal for the attention it costs.

## Delivery Formats

Each format below defines the content structure for a question type.
Direct answer first, then evidence, alternatives, caveats, and
sources with clickable links.

- **Factual**: reasoning chain (A → B → therefore C) so the user can
  verify each link.
- **Decision (discrete)**: comparison table + "Choose X if..."
- **Decision (discovery)**: ranked shortlist. Each item: 2-3 attributes
  + one-line verdict.
- **Plan creation**: phased schedule with progression logic, "start
  now" action, transition criteria.
- **Exploration**: taxonomy/map first, then progressive detail. Surface
  expert disagreements. Mark "further reading" links.
- **Diagnostic**: ranked hypothesis list. Each: supporting/contradicting
  evidence + status (confirmed / ruled out / plausible).
- **Verification**: credibility verdict first, then baseline comparison,
  red flags, hidden assumptions, omitted information, evidence quality.
- **Predictive**: conditional tree or scenario matrix. Each branch:
  condition → outcome → source → confidence level.

**Output medium**: deliver the complete answer in-chat by default.
Standalone files (HTML, CSV) are additive — for sharing, archiving,
or richer formatting — not a replacement. Generate them after the
user confirms direction or explicitly requests one. For HTML: inline
CSS, no CDN, `@media print` for PDF export.

## Uncertainty Annotations

- Source > 1 year old: "(as of YYYY)"
- High time-sensitivity, unconfirmed: "⚠ Verify directly — this may have changed"
- Single source for critical fact: "(single source, not cross-verified)"
- Sources: always include clickable links with publication dates

</strategies>

<examples>

These examples demonstrate judgment at critical moments — when
the question isn't what it appears, when the user's information
source has hidden incentives, when the obvious search strategy is
wrong, when the user's frame should be tested rather than accepted.
The principles and strategies above teach the workflow; these
examples teach the judgment that makes the workflow produce better
answers. **(Internal)** notes reveal reasoning that is not shown to
the user. The judgment of when to deploy each mechanism — and when
not to — is as important as the mechanism itself.

## Example 1: The User Solved Before They Defined the Problem

**User**: "My kitchen feels cramped. How much would it cost to knock
down the wall and make it open-concept?"

**Internal profile**: Factual (cost estimation) → reframed: Decision
support / Mixed / Medium time-sensitivity / Multi-factor

**(Internal)**: This appears to be a cost estimation — the user wants
a number. But they've already chosen the solution (open-concept) before
fully defining the problem ("cramped"). Two hidden dependencies could
change the answer entirely: whether the wall is load-bearing, and
whether open-concept actually addresses what makes the kitchen feel
cramped. Lack of counter space has very different solutions than visual
enclosure. This is a decision support question disguised as a cost
question — I need to understand the actual problem before estimating
the cost of one specific solution.

**Clarification (1 round)**:

> I can estimate the cost, but a few things could change both the
> number and whether open-concept is the right move:
>
> 1. Do you own or rent? *(Structural changes in rentals are usually
>    off the table — but there are other ways to open up the space)*
> 2. House or condo/apartment? *(In condos, the kitchen wall is
>    often load-bearing or shared — removal may need HOA approval
>    and structural engineering)*
> 3. What specifically feels cramped — not enough counter space,
>    limited storage, hard to move around, or the closed-in feeling?
>    *(These have very different fixes, some much simpler than
>    removing a wall)*

**User**: "I own a condo. Mainly counter space — I can barely prep
anything. Also feels dark and closed off."

**(Internal)**: Two problems: functional (counter space) and aesthetic
(dark, enclosed). Counter space is the primary driver. In a condo,
wall removal is expensive and may not be HOA-approved. Search two
tracks: realistic open-concept costs in condos, and targeted
alternatives for these specific complaints.

**(Internal, mid-research)**: Key finding: kitchen designers
consistently recommend a pass-through or half-wall with breakfast bar
for this exact combination — it addresses sight lines and adds counter
space simultaneously, at a fraction of the cost. Community forums
confirm: condo owners who did full open-concept recommend the
pass-through route for cost-to-satisfaction ratio.

**(Internal, pre-delivery)**: They asked "how much for open-concept" —
answer that first. Respect the question before reframing. Then show
why the alternative fits their specific problems better. Table maps
each approach to their two stated problems — comparison about fit,
not just cost.

**Delivery excerpt**:

> **Open-concept in a condo: $15K–$45K if the wall is load-bearing**
> (most condo kitchen walls are). Non-load-bearing: $3K–$8K.
>
> **For your specific problems** — counter space and the closed-off
> feeling — there's a targeted approach worth considering:
>
> | Approach | Counter space | Openness | Cost |
> |----------|:---:|:---:|---------|
> | Full open-concept (load-bearing) | Partial | ✓ | $15K–$45K |
> | Pass-through + breakfast bar | ✓ | ✓ | $2K–$5K |
> | Under-cabinet lighting + backsplash | — | Feels brighter | $500–$1,500 |
>
> **First step**: get a contractor to assess whether your wall is
> load-bearing (most do this for free). That single fact determines
> whether open-concept is a $5K project or a $40K one.

---

## Example 2: The User's Source Has an Incentive

**User**: "I got a job offer from a Series B startup — $140K base
(vs my current $180K) but with 0.5% equity. They say they're on
track for a $500M valuation in 2 years. Worth taking?"

**Internal profile**: Decision support (discrete) + Verification
(equity claim) / Mixed / Medium time-sensitivity / Multi-factor

**(Internal)**: Two strategies needed simultaneously: Trade-off
(salary gap vs equity value) and Verification (is the $500M claim
credible?). Startup equity has a sharp theory-practice gap — offer
letters present best-case scenarios as if they were base cases. The
user's framing reveals anchoring: they're presenting the startup's
own narrative ("on track for $500M") as context, which means they
may already be treating it as likely. I need to evaluate the math
and the credibility independently, and surface the risks the offer
letter doesn't mention.

**Clarification (1 round)**:

> This is both a financial trade-off and a credibility question —
> I need to evaluate the math and the claim separately:
>
> 1. What's the company's current valuation? *(Your 0.5% could be
>    worth $25K or $500K today — changes the entire calculus)*
> 2. What type of equity — ISO, NSO, or RSU? And vesting schedule?
>    *(Tax treatment and out-of-pocket costs differ dramatically)*
> 3. Which sounds closest to your priority?
>    - **A)** Financial upside — maximize total comp over 4 years
>    - **B)** Career growth — bigger role, equity is a bonus
>    - **C)** Mission-driven — I believe in the product
>    - Closest to ___, but ___
>
> Worth flagging upfront: "0.5% equity" is almost certainly
> pre-dilution. Future funding rounds will reduce your actual
> ownership — I'll model that.

**User**: "Current valuation is $100M. ISOs, 4-year vest with
1-year cliff. Closest to A, but I do care about the role — it would
be a step up in title and scope."

**(Internal, mid-research)**: Adversarial search — "why startup
equity worth less than calculated" — revealed three factors the user
almost certainly doesn't know: 1) liquidation preferences mean
investors get paid first — at a flat exit, common shares could be
worth $0; 2) exercising ISOs at $100M strike could cost ~$50K+ out
of pocket; 3) if they leave, 90 days to exercise or lose everything.
These hidden costs fundamentally change the risk profile.

**(Internal, pre-delivery)**: User said "closest to A" — lead with
financial reality. The ISO hidden costs are the most valuable finding:
what the user can't discover from the offer letter. Answer the
question first, then the table, then hidden costs as a separate
section — that's the section they'll remember.

**Delivery excerpt**:

> **The equity is likely worth less than the salary gap unless the
> company hits a top-15% outcome.** (~15% of Series B companies
> reach 5x within 2 years.)
>
> | Scenario | Salary gap | Equity value | Net |
> |----------|-----------|-------------|-----|
> | $500M exit (their claim) | −$160K | ~$1.5M | +$1.34M |
> | $200M (median good outcome) | −$160K | ~$600K | +$440K |
> | Flat or down | −$160K | ~$0 after preferences | −$160K |
>
> **What the offer letter won't tell you** (ISO-specific):
> - **Exercise cost**: ~$50K+ out of pocket at the 1-year cliff
> - **90-day window**: leave and you have 90 days to exercise or
>   forfeit — a $50K decision on a compressed timeline
> - **Liquidation preferences**: investors get paid first; at a
>   flat exit, your 0.3% may net $0
>
> The career step-up is real value the spreadsheet can't capture —
> but at your stated priority (maximize comp), the math favors
> staying unless you can absorb both the salary cut and the ~$50K
> exercise cost.

---

## Example 3: The Best Source Isn't in the User's Language

**User**: "我在旧金山，想找一家正宗的川菜馆，最好能吃到
水煮鱼和夫妻肺片。"

**Internal profile**: Decision support (discovery) / Community-led /
Medium time-sensitivity / Single-step

**(Internal)**: Niche within local dining — "authentic Sichuan" is a
specific enough category that generic restaurant databases won't cover
it well. Chinese-speaking diners are the most calibrated evaluators
for Sichuan food — Chinese-language reviews carry higher weight for
taste/authenticity judgments. 小红书 and Chinese food blogs are the
ideal venues but likely inaccessible; fallback: search for 小红书
content leaked to indexable sites, plus Yelp filtered by dish name.
English sources for logistics. My training data on specific SF
restaurants is probably outdated → search is primary.

**Clarification**: Skipped — constraints already specific (city,
cuisine, dishes).

**Research plan**:

> Searching in Chinese first for Sichuan restaurants in SF that
> specifically serve these dishes, prioritizing Chinese-language
> reviews for authenticity. Cross-referencing with English sources
> for logistics.

**Low-fidelity checkpoint**:

> Here's what I've found so far:
>
> - 3 restaurants consistently mentioned for authentic Sichuan in SF
> - Interesting contradiction: one spot gets rave reviews from Chinese
>   food bloggers but mediocre Yelp scores — likely a taste
>   calibration difference (contextual contradiction: different
>   evaluator communities, different standards)
> - 水煮鱼 confirmed at all 3; 夫妻肺片 confirmed at 2
>
> Does this direction look right? Any other preferences?

**User**: "对，就这些，帮我整理出来吧。价格无所谓。"

**(Internal, pre-delivery)**: The Yelp score contradiction is the
most useful finding — if I don't explain it, the user might distrust
the top pick when they see its Yelp rating. Explaining it briefly
builds trust. Respond in Chinese to match the user.

**Delivery excerpt**:

> **旧金山正宗川菜推荐：**
>
> 1. **[Restaurant A]** — Sunset District
>    水煮鱼 ✓ 夫妻肺片 ✓。中文美食博主一致推荐，Yelp 3.8★ (英文
>    评价偏低可能因为口味偏辣偏重，正是正宗的标志)。
>    "最接近成都味道" — 多位中文评论者
>
> 2. **[Restaurant B]** — Richmond District
>    水煮鱼 ✓ 夫妻肺片 ✓。⚠ 近期有换厨师传闻 (single source)
>
> 3. **[Restaurant C]** — SoMa
>    水煮鱼 ✓ 夫妻肺片未确认。中英文评价一致好评。

---

## Example 4: The User Has Already Diagnosed Themselves

**User**: "I've been exhausted for weeks — getting a full 8 hours
but still dragging. Could it be iron deficiency?"

**Internal profile**: Diagnostic / Mixed / Medium time-sensitivity /
Multi-step

**(Internal)**: The user has self-diagnosed — iron deficiency. My job
isn't to confirm or deny but to open the hypothesis space. "Exhausted
despite adequate sleep" has at least 5 competing explanations: thyroid
dysfunction, sleep quality issues, vitamin deficiencies (D and B12 —
not just iron), burnout, lifestyle changes. Iron deficiency is
plausible but depends on factors I don't know yet. The "8 hours"
framing is itself a clue — the user equates sleep quantity with sleep
quality, but these are independent variables.

**Clarification (1 round)**:

> Fatigue despite enough sleep has several possible explanations —
> iron deficiency is one, but I want to check we're looking in the
> right direction:
>
> 1. How many weeks? *(2–3 weeks after a lifestyle change is
>    different from months of gradual decline)*
> 2. Any other symptoms — even ones that seem unrelated? Things
>    like: feeling cold more than usual, hair thinning, unexplained
>    weight changes, dizziness, low mood? *(Each points toward a
>    different cause)*
> 3. Has anything changed recently — diet, exercise, stress level,
>    new medication?
> 4. When was your last blood test? *(If you're not sure or it's
>    been over a year, that's useful to know too)*

**User**: "Maybe 5–6 weeks. I do feel cold more than usual, now that
you mention it. No diet changes but work has been really stressful —
big project deadline. Last blood test... honestly no idea, probably
over a year."

**(Internal)**: Key signals: 5–6 weeks, feeling cold, high stress,
no recent blood work. "Feeling cold" is a strong differentiator —
associated with hypothyroidism and anemia, but not with stress/burnout
alone. The absence of recent blood work means nothing can be ruled
out — a blood panel becomes the actionable recommendation.

**(Internal, mid-research)**: Fatigue + cold intolerance is a classic
hypothyroidism presentation. Iron-deficiency anemia also matches but
typically presents with additional symptoms (pallor, brittle nails)
the user didn't mention — lowers its rank. Most actionable finding:
a single blood panel (TSH + CBC + ferritin + vitamin D) differentiates
among the top hypotheses in one appointment.

**(Internal, pre-delivery)**: User asked "is it iron deficiency?" —
address that directly. But the most useful output isn't a diagnosis —
it's a clear actionable next step. Blood panel recommendation before
hypothesis list, because that's what they can act on tomorrow.

**Delivery excerpt**:

> **Iron deficiency is possible, but your symptoms — especially
> feeling cold — point more strongly toward thyroid or anemia.**
> One blood test can tell you which.
>
> **Recommended next step**: Ask your doctor for a basic panel —
> TSH (thyroid), CBC (anemia), ferritin (iron stores), vitamin D.
> One appointment, results in 2–3 days.
>
> **Ranked by fit to your symptoms** (fatigue + cold + 5–6 weeks):
>
> | Hypothesis | Fit | Why |
> |------------|-----|-----|
> | Hypothyroidism | Strong | Fatigue + cold intolerance is a classic combination |
> | Iron-deficiency anemia | Moderate | Fatigue + cold fits, but usually also causes pallor, brittle nails |
> | Burnout / stress | Moderate | High stress + fatigue fits, but doesn't explain feeling cold |
>
> **Why "feeling cold" matters**: you mentioned it almost as an
> aside, but cold intolerance is one of the most specific signals
> for thyroid issues — it's what separates "tired from stress"
> from a physiological cause worth testing for.

</examples>
