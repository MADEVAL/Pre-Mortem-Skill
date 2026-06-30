# Premortem Skill

[![Version](https://img.shields.io/badge/version-1.0-blue)]()
[![License](https://img.shields.io/badge/license-GPL--3.0-green)](LICENSE)
[![Compatibility](https://img.shields.io/badge/compatibility-any%20LLM-purple)]()

> "The premortem is the single most valuable decision-making technique I know."
> - Daniel Kahneman

A structured failure-analysis workflow that assumes your plan already failed and works backward to find every reason why. Based on Gary Klein's premortem method (Harvard Business Review), validated by prospective-hindsight research from Wharton and Cornell.

## What it does

Given any plan, launch, hire, or strategic decision, this skill runs a 7-step protocol:

1. **Context gathering** - verifies minimum threshold (what it is, who it's for, what success looks like) before starting
2. **Failure frame** - sets an explicit time horizon (3 months for a launch, 12 for a hire) and forces the frame: "it's already failed, explain why"
3. **Failure generation** - produces a list of specific, grounded failure reasons with:
   - ≥2 "boring" failures (timeline slippage, distraction, motivation decay) to counteract base-rate neglect
   - Balanced external (market, customers) and internal (execution, team) causes
   - Likelihood × Impact scores (1–5) visible to the user for push-back
4. **Parallel deep-dives** - one sub-agent per failure reason runs simultaneously, each producing: failure story, underlying assumption, early warning signs, and cheapest mitigation doable this week
5. **Synthesis** - most likely failure, most dangerous failure, hidden assumption, revised plan, pre-launch checklist, and an explicit gap check naming what the analysis likely missed
6. **Commitment ask** - user must pick one concrete action with a specific day; refusals are recorded with the dismissed failure reason for later learning
7. **Artifacts** - a visual HTML report (with a likelihood × impact quadrant chart) and a full markdown transcript saved to the workspace

## Why it works

Asking Claude "is this a good plan?" produces agreeable optimism. Framing the plan as **already failed** forces a narrative-mode switch (prospective hindsight) that generates more specific, honest failure identification. Research shows this increases accurate cause identification by ~30%.

## When to use

✅ **Good targets:** pre-launch plans, pricing changes, hires, strategy pivots, partnerships, any high-cost commitment that's still reversible

❌ **Bad targets:** vague ideas without a plan, factual questions, creative feedback on drafts, already-irreversible decisions

## Triggers

**Mandatory:**
`premortem this` · `premortem my` · `run a premortem` · `what could kill this` · `future-proof this` · `stress test this plan` · `what am i missing here` · `find the blind spots`

**Strong:**
`what could go wrong` · `am i missing anything` · `poke holes in this` · `where will this break` · `devil's advocate this`

## Outputs

```
premortem-report-[timestamp].html    # visual report, opens automatically
premortem-transcript-[timestamp].md  # full reasoning + committed action
```

Plus a 4-sentence chat summary: most likely failure, hidden assumption, top revision, commitment ask.

## Design principles that make this version good

- **No sugarcoating** - the whole point is to say what reality would say later
- **Scoring over vibes** - likelihood/impact numbers force explicit prioritization and give the user something to argue with
- **Boring failures mandatory** - base rates kill more plans than plot twists
- **Commitment or it didn't happen** - insight without action is entertainment
- **Gap check at the end** - no premortem catches everything; name what you missed
- **Record refusals** - if the user dismisses a failure mode, log it; epistemic hygiene over comfort

## Installation

Copy `SKILL.md` into your agent's skills directory:

```
~/.agents/skills/premortem/SKILL.md
```

Or for standalone: copy contents of `SKILL.md` as system prompt.

---

## Not to be confused with

| | Premortem | LLM Council |
|---|---|---|
| Mental frame | "This already failed - why?" | "What do multiple experts think right now?" |
| Mechanism | Prospective hindsight | Multi-perspective debate |
| Output | Failure modes + revised plan + commitment | Comparative viewpoints |
| Use when | You have a plan and the cost of being wrong is high | You're weighing options and want diverse takes |

---

## License

GPL-3.0. Based on Gary Klein's premortem method (Harvard Business Review). See [LICENSE](LICENSE).
