# Bloom — teaching AI to understand before it answers

The quality of AI answers is largely a human-AI interaction problem.

Ask AI a hard question and it answers immediately — confident, well-structured, and built on assumptions about your situation it never checked. The answer sounds right. When it's not, it doesn't just miss — it can send you in entirely the wrong direction.

I'm a designer. The first principle of design thinking is: defining the right problem matters more than finding the right solution. The same principle shows up in every good lawyer, doctor, and consultant — they all evolved toward the same pattern: understand the person's situation first, then advise. This isn't just professional courtesy. It's the only way to give answers that actually fit.

Current AI skipped this step. The chatbot paradigm — ask once, get a complete answer — is a step backward from what human professionals learned over centuries.

Bloom is an attempt to correct that.

## How it works

The idea: teach AI to clarify your situation before researching, and research before answering — so the answer fits your specific case, not just the general one. The entire product is one file: [SKILL.md](skills/bloom/SKILL.md). No code, no API keys, no dependencies. Just a carefully designed prompt you can read in a few minutes.

The workflow:

- **Clarify** — targeted questions about your specific situation (only what would change the answer)
- **Plan** — proposes a research approach you can review
- **Research** — official sources + community experiences, cross-referenced
- **Deliver** — conclusion first, evidence and sources after

> **Built for questions like:** Should I buy or rent in NYC on my salary? · My landlord is raising rent 15% — what are my rights? · Comparing 3 health insurance plans — which is cheapest for my situation? · $180K base vs $140K + equity — which job offer is worth more? · Freelancing while employed — what should I watch out for? · Japan trip with a toddler — what's realistic?

## Same question, different first move

> "My landlord is raising rent 15%. What are my rights?"

**ChatGPT 5.4 Thinking** answered immediately with a detailed legal document — for Hoboken, New Jersey. It had pulled a friend's address mentioned in a previous conversation. However, the user lives in New York City 🫠... Different city, different state, entirely different tenant protection laws. Confident, thorough, and wrong.

**Bloom** asked four questions first: *What state and city? What type of lease? How much notice did they give? Is your building rent-stabilized?* Then researched the user's actual jurisdiction.

See the [full conversation comparison](docs/comparison.md) for the complete exchange and final output.

## Quick start

Clone the repo or download ZIP from [GitHub](https://github.com/woody-design/bloom-deep-research):

```bash
git clone https://github.com/woody-design/bloom-deep-research.git
```

**Claude desktop app (Cowork):**

1. Open the Claude desktop app
2. Go to **Settings** → **Plugins**
3. Click **Install from folder…**
4. Select the `bloom-deep-research` folder

**Cursor:** use `SKILL.md` directly as an agent skill.

Then:

```
/bloom Should I register my LLC in New York or New Jersey?
```

Bloom will ask clarifying questions, propose a research plan, then deliver a structured answer tailored to your situation.

## Design decisions

**Ask, don't infer.** If information matters to the answer, ask — don't infer. A wrong inference is the most dangerous kind of error: invisible to the user, impossible to correct. The design work goes into making questions effortless to answer — not into avoiding them.

**Downgrade the cost of every question.** "What's your experience level?" requires self-assessment. "How many times a week do you train?" requires recall. Same information, radically different cost to the user. Every question is redesigned to ask less of the person answering it.

**The conflict is the finding.** When sources disagree, don't split the difference — find the condition that makes both right. That condition is often the most valuable part of the answer.

**Share rough, deliver on readiness.** The first output after research is deliberately rough — key findings, contradictions, open questions. A polished answer signals "finished" and shuts down the conversation the user needs to get the direction right. The full version comes when they're ready — not when the AI is.

**Principles over procedures.** As models get more capable, detailed instructions stop helping and start constraining. Bloom teaches how to think about a problem — not what steps to follow. The goal: prompt engineering that looks more like mentorship than programming.

## Known limitations

Bloom is a single-session research skill. Multi-turn iteration (coming back to refine after delivery) relies on the model's default behavior and isn't explicitly designed yet. Feedback on real-world edge cases is the most valuable contribution you can make.

## Contributing

Issues and PRs welcome. If you have ideas for improving the research workflow, [open an issue](https://github.com/woody-design/bloom-deep-research/issues).

## License

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — free for any use, including commercial, with attribution. Derivatives must use the same license.

By Woody Li — designer & AI cocreator.