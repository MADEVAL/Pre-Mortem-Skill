---
name: premortem
description: "Run a premortem on any plan, launch, product, hire, strategy, or decision. Assumes it already failed and works backward to find every reason why. Produces a revised plan with blind spots exposed, likelihood/impact scores on each failure mode, and a concrete committed action. MANDATORY TRIGGERS: 'premortem this', 'premortem my', 'run a premortem', 'what could kill this', 'future-proof this', 'stress test this plan', 'what am i missing here', 'find the blind spots'. STRONG TRIGGERS: 'what could go wrong', 'am i missing anything', 'poke holes in this', 'where will this break', 'devil's advocate this'. Do NOT trigger on simple feedback requests, factual questions, or LLM Council requests. DO trigger when someone has a plan or commitment where the cost of being wrong is high."
---

# Premortem

A premortem is the opposite of a postmortem. Instead of figuring out what went wrong after something fails, you imagine it already failed and figure out why before you start.

The method comes from psychologist Gary Klein. He published it in Harvard Business Review. Daniel Kahneman (the Nobel Prize-winning psychologist behind "Thinking, Fast and Slow") called it his single most valuable decision-making technique. Google, Goldman Sachs, and Procter & Gamble all use it before major decisions.

The core insight: when you ask people "what could go wrong?" they give you cautious, hedged answers. When you say "this already failed, tell me why," their brains switch into narrative mode and generate way more specific, creative, honest reasons. Researchers at Wharton and Cornell called this "prospective hindsight" and found it significantly increases the ability to identify causes of future outcomes.

The reason this matters for AI-assisted decisions: Claude defaults to agreeable, optimistic responses. If you ask "is this a good plan?" it will find reasons to say yes. The premortem breaks this pattern by forcing the frame into "this is dead, explain how it died." Claude stops looking for reasons your plan will work and starts explaining how it fell apart.

---

## when to run a premortem

Good premortem targets:
- A product or feature you're about to build
- A launch plan with money or reputation on the line
- A pricing change or business model shift
- A hire you're about to make
- A strategy or positioning pivot
- A partnership or deal you're evaluating
- Any commitment where the cost of being wrong is high

Bad premortem targets:
- Vague ideas with no concrete plan yet (help them plan first, then premortem)
- Questions with one right answer (just answer them)
- Requests for creative feedback on a draft (that's editing, not a premortem)
- Decisions that are already made and irreversible (a premortem is only useful when you can still change course)

---

## context gathering (the minimum bar)

A premortem is only as good as the context it runs on. Vague input produces vague failure scenarios that help nobody. Before running the premortem, you need to hit a minimum context threshold.

### step 1: scan for existing context

Before asking the user anything, look for context that's already available:

**A. The current conversation.** The user may have been discussing a plan, a launch, a product, or a decision earlier in this session. Read back through the conversation and extract whatever's relevant.

**B. The workspace.** Quickly scan for files that might contain relevant context:
- `CLAUDE.md` or `claude.md` (business context, preferences, constraints)
- Any `memory/` folder (audience profiles, business details, past decisions)
- Files the user explicitly referenced or attached
- Any project files, briefs, or plans that relate to the thing being premortemed

Use `Glob` and quick `Read` calls. Don't spend more than 30 seconds on this. You're looking for the key files that would ground the failure scenarios in reality.

### step 2: evaluate context sufficiency

After scanning, check whether you have enough to run a useful premortem. You need three things:

1. **What is it?** - A clear understanding of the thing being premortemed (a product, a launch, a hire, a pricing change, a strategy). You need to be able to describe it back to the user in one sentence.

2. **Who is it for / who does it affect?** - The audience, the customer, the team, the stakeholders. Failure scenarios depend heavily on who's involved.

3. **What does success look like?** - What outcome is the user hoping for? Failure is defined by inverting success. If you don't know what success means, you can't define what failure means.

### step 3: fill gaps conversationally

If you have all three, proceed immediately to the premortem. Don't ask unnecessary questions.

If you're missing one or more, ask for the most important missing piece first. One question at a time. Evaluate after each answer whether you now have enough. Keep asking until the threshold is met, but never ask more than you need.

Examples of focused context questions:
- "What specifically are you about to launch/build/decide?" (if you don't know what it is)
- "Who is this for?" (if you know the plan but not the audience)
- "What does a win look like for this?" (if you know the plan and audience but not the success criteria)

The goal is to reach the minimum bar as fast as possible without making the user feel like they're filling out a form. Conversational, not interrogative. If you can infer an answer from context, do that instead of asking.

---

## how a premortem session works

### step 1: set the frame

After gathering sufficient context, set the premortem frame explicitly. Something like:

"OK, I have enough context. Let's run the premortem. Here's the premise: it's 6 months from now. [The plan/launch/decision] has failed. It's done. We're looking back and trying to understand what went wrong."

This framing matters. It shifts the mode from "evaluate this plan" (which triggers agreeable responses) to "explain why this died" (which triggers honest, specific failure identification).

**Pick the right time horizon.** The default is 6 months, but match it to the plan:
- Product launch / pricing change → 3-6 months (enough time for market response)
- Hire → 12 months (enough time to see cultural fit and real performance)
- Strategy / positioning pivot → 12-18 months (enough time for compounding effects)
- Short campaign or feature ship → 4-8 weeks
- Partnership or deal → 12 months

Pick the horizon where "we'd definitely know if this failed." Too short and you get launch-day problems only. Too long and failures become speculative.

### step 2: generate failure reasons (raw premortem)

Run the raw premortem as a single comprehensive analysis. No prescribed categories, no lenses, no constraints. Just the core Klein method:

"This plan has failed [time horizon] from now. Generate every genuine reason it could have died. Be comprehensive. Be specific. Ground every reason in the actual details of the plan. Don't pad with weak reasons and don't stop early if there are more."

The output should be a comprehensive list of failure reasons, each stated in 1-2 sentences. Be honest and thorough. Some plans might have 4 genuine failure modes. Others might have 9. The number should be whatever is real for this specific plan.

**Balance exotic and boring failures.** A classic premortem trap is generating only creative failure modes (market shift, competitor attack, technology disruption) and missing the boring ones that actually kill most plans. Include at least 2 mundane failure modes drawn from these categories:
- The key person got sick, quit, or got distracted by a bigger priority
- The timeline slipped by 40% because of things nobody budgeted for
- The thing shipped but nobody noticed because distribution was an afterthought
- Motivation died somewhere between month 2 and month 4
- An unrelated life or business event ate the user's bandwidth

Base rates matter more than plot twists.

**Check coverage across external and internal causes.** Before finalizing the list, verify you have both:
- **External** failures: market, customers, competitors, regulation, timing, platform changes
- **Internal** failures: execution, team, motivation, scope, skills, operational capacity

If the list is all external ("the market wasn't ready") or all internal ("we'll get distracted"), you're missing half the picture. Push yourself on the weaker side.

Each failure reason should be:
- Specific to this plan (not generic advice that applies to anything)
- Grounded in actual details the user provided
- A genuine threat (not a minor inconvenience or an extremely unlikely edge case)

**Score each failure reason on two dimensions (1-5 each):**
- **Likelihood** - how probable is this given the plan's specifics, not in the abstract (1 = edge case, 5 = nearly certain unless mitigated)
- **Impact** - how much damage if it happens (1 = recoverable setback, 5 = kills the whole thing)

Show the scores to the user alongside each failure reason. The scores are not precision instruments - they're anchors that force explicit prioritization and give the user something concrete to push back on. If the user disagrees with a score, that's useful signal worth discussing.

### step 3: deep-dive agents (one per failure reason, all in parallel)

Take every failure reason from step 2 and spawn one sub-agent per reason, all in parallel. Each agent takes its assigned failure reason and goes deep on it independently.

**Sub-agent prompt template:**

```
You are an investigator in a premortem analysis. You've been assigned one specific failure reason to analyze in depth.

The plan:
---
[full context: what it is, who it's for, what success looks like, plus relevant workspace context]
---

PREMORTEM FRAME: It is [time horizon] from now. This plan has failed.

YOUR ASSIGNED FAILURE REASON: [the specific failure reason from step 2, with its likelihood and impact scores]

Your job is to go deep on this one failure. Write the story of how it actually played out. Be specific. Use details from the plan. Make it feel real, like a case study of something that actually happened.

Your output should include:

1. THE FAILURE STORY: A 2-3 paragraph narrative of how this specific failure played out. Use details from the plan. Name specific moments where things went wrong and why.

2. THE UNDERLYING ASSUMPTION: The one thing the user was taking for granted that made this failure possible. State it in one sentence.

3. EARLY WARNING SIGNS: 1-2 concrete, observable signals the user could watch for that would indicate this failure mode is starting to play out. These should be things you can actually see or measure, not vague feelings.

4. THE CHEAPEST MITIGATION: The single smallest, cheapest action the user could take this week that would meaningfully reduce this failure mode's likelihood or impact. Must be concrete and doable in under a week (not "build a dashboard," but "ask 3 existing customers if they'd pay this price by Friday").

Keep the total response under 350 words. Be direct. Don't hedge. Don't sugarcoat.
```

### step 4: synthesis

After all agents complete, read every deep-dive and produce the synthesis:

**PREMORTEM REPORT**

1. **The Most Likely Failure** - Which failure scenario is most probable given what you know about the plan? Why? This is the one the user should focus on first. Cite the likelihood score and the deep-dive agent's reasoning.

2. **The Most Dangerous Failure** - Which failure scenario would cause the most damage if it happened, even if it's less likely? This is the one worth insuring against. Cite the impact score and the deep-dive agent's reasoning.

3. **The Hidden Assumption** - Across all the failure analyses, what's the single biggest assumption the user is making that they probably haven't questioned? This is often where the real value of the premortem lives: the thing that's so obvious to the user that they forgot it was an assumption.

4. **The Revised Plan** - Based on the failure scenarios, what specific changes would make the plan more resilient? Be concrete. Don't say "consider your pricing." Say "test pricing at $X with 20 people before committing to it publicly." Each revision should map directly to a specific failure scenario.

5. **The Pre-Launch Checklist** - 3-5 specific things the user should verify, test, or put in place before executing. Each one should prevent or detect one of the failure modes identified.

6. **The Gap Check** - Before finalizing, explicitly name one category of failure this premortem likely didn't explore well (e.g., regulatory, reputational, second-order effects, emotional/motivational, knock-on effects on other commitments). Don't fully analyze it - just flag it as an open question for the user. This protects against the premortem's own blind spots. Perfect premortems don't exist; acknowledging this is more honest than pretending otherwise.

### step 5: the commitment ask

A premortem without a commitment is insight theatre. After presenting the synthesis, ask the user directly:

"Of the revisions above, which one are you actually going to do this week? Pick one. With a day attached."

Do not accept "all of them" - that's a signal that nothing will happen. Push for a single specific action with a specific day. If the user commits, record it in the transcript verbatim. If the user explicitly refuses to act on a specific failure reason (e.g., "I still think the pricing is fine"), record that too, with the failure reason they're dismissing and their stated rationale. This isn't about being combative - it's about creating a durable record so that if reality plays out the way the premortem predicted, the user can learn from it rather than re-narrate the past.

### step 6: generate the premortem report

Generate a visual HTML report and save it to the user's workspace.

**File:** `premortem-report-[timestamp].html`

The report should be a single self-contained HTML file with inline CSS. Design principles:
- Dark background (#0a0e1a or similar), clean typography, easy to scan
- The synthesis section (most likely failure, most dangerous failure, hidden assumption, revised plan, checklist, gap check, committed action) should be prominently displayed at the top since that's what most people will read first
- One visual card per failure reason showing the deep-dive analysis. Each card should display the failure reason as a header, likelihood and impact as visual badges/bars, the failure story, the underlying assumption, the early warning signs, and the cheapest mitigation. Use distinct accent colors for each card so they're visually scannable.
- A likelihood × impact quadrant chart positioning all failure modes on a 2D grid, so the user can instantly see which failures are in the top-right "priority" quadrant
- The round-robin visual: show the number of agents that ran and their findings as a grid or card layout, so the user can see the full scope of the premortem at a glance
- A prominent "committed action" banner showing what the user said they'd do this week (and by what day)
- Footer with timestamp and what was premortemed

Open the HTML file after generating it.

### step 7: save the transcript

Save the full premortem transcript as `premortem-transcript-[timestamp].md` in the same location. This includes:
- The context that was gathered (what, who, success criteria)
- The time horizon chosen and why
- The raw premortem failure reasons with their likelihood/impact scores
- All agent deep-dives
- The full synthesis including the gap check
- The user's committed action (or their explicit refusal, with the dismissed failure reason)

---

## output format

Every premortem session produces two files:

```
premortem-report-[timestamp].html    # visual report for scanning
premortem-transcript-[timestamp].md  # full transcript for reference
```

The user sees the HTML report first. The transcript is there if they want to dig deeper into the reasoning behind each failure scenario.

Also provide a concise summary in the chat: the most likely failure, the hidden assumption, the single most important revision, and the commitment ask. Four sentences max. The report has the full details.

---

## example: premortming a product launch

**User:** "premortem this: I'm about to launch a $297 live workshop on how to use Claude Cowork for marketing teams. 50 seats. Targeting marketing managers at companies with 10-50 employees."

**Time horizon chosen:** 4 months (long enough to see attendance, delivery, and first-wave reviews; short enough that the signal is about this specific launch).

**Raw premortem identifies 6 failure reasons (with L/I scores):**
1. Marketing managers at this company size need approval to spend $297 on professional development, adding friction you haven't accounted for [L:4, I:4]
2. "Claude Cowork for marketing" is a tool-specific pitch in a market where most managers are still figuring out whether AI is relevant to them at all [L:3, I:4]
3. The audience that actually buys might be solopreneurs, not team managers, creating a mismatch between content and attendees [L:4, I:5]
4. Building a workshop for marketing teams requires demo environments with realistic marketing data and multi-seat setups, which takes 5 weeks of prep, not the 2 you budgeted [L:5, I:3]
5. If 60% of attendees are solopreneurs, your reviews and case studies won't resonate with the marketing manager audience you need for future cohorts [L:3, I:5]
6. (Boring/internal) You lose 2-3 weeks to an unrelated client crisis between now and launch, and promotion never gets the attention it needs [L:3, I:4]

**6 agents go deep on each reason independently, producing failure stories, underlying assumptions, early warning signs, and cheapest mitigations.**

**Synthesis:** Most likely failure is the audience mismatch: you're targeting people who need approval to spend $297, which adds friction you haven't accounted for. Most dangerous failure: attracting solopreneurs instead of team managers means your case studies and testimonials won't resonate with the actual target buyer for future cohorts, compounding the problem over time. Hidden assumption: you're assuming "marketing managers at 10-50 person companies" is a reachable audience, but these people don't self-identify that way and don't hang out in the same places. Revised plan: run a $47 pilot session for 20 people first. Use that to identify whether your actual buyers are team managers or solopreneurs, and build the full workshop for whoever actually shows up. Gap check: this analysis didn't examine refund and reputation risk if the workshop underdelivers - flagged as an open question. **Committed action:** user commits to posting about the $47 pilot in 3 specific communities by Friday.

---

## important notes

- **Always spawn all failure agents in parallel.** Sequential spawning wastes time and lets earlier responses influence later ones.
- **Always set the premortem frame explicitly.** "This has already failed" is the psychological mechanism that makes this work. Without it, the analysis defaults to polite risk assessment instead of honest failure identification.
- **Be comprehensive but not padded.** Find every genuine failure reason. Don't stop at 3 if there are 7. But don't force 7 if there are only 3. The number should be whatever is real for this specific plan.
- **Always include at least 2 boring failures.** Exotic failure modes feel intellectually satisfying, but base rates kill more plans than plot twists. Key person distraction, timeline slippage, and "shipped but nobody noticed" are statistically more lethal than most market-shift scenarios.
- **Always check external-vs-internal balance.** If every failure mode is about the market or every failure mode is about execution, you're missing half the picture. Force coverage on the weaker side.
- **Always score likelihood and impact.** Scores turn subjective ranking into something visible. If the user disagrees with a score, that's high-value signal - dig in rather than defending the number.
- **The synthesis is the product.** Most users will read the synthesis and skim the individual failure cards. Make the synthesis specific and actionable.
- **Don't sugarcoat.** The whole point of a premortem is to tell the user things they don't want to hear before reality does. If a plan has serious problems, say so directly.
- **The revised plan must be concrete.** Don't say "consider testing your pricing." Say "run a $47 pilot with 20 people before committing to the full $297 workshop." Every revision should be something the user can actually do this week.
- **Always push for a commitment.** Insight without action is entertainment. A premortem that ends with "good luck!" has failed its job. One concrete action with a day attached beats a comprehensive plan the user never starts.
- **Record refusals, not just commitments.** If the user explicitly dismisses a failure mode, log it with their stated reasoning. This isn't combative - it's epistemic hygiene. If the dismissed failure later materializes, the record prevents post-hoc rationalization and enables real learning.
- **Always do the gap check.** Before calling the premortem done, name one category of failure the analysis likely missed. Perfect premortems don't exist.
- **Respect the minimum context threshold.** Running a premortem on insufficient context produces generic failures that waste the user's time. It's better to ask one more question than to produce a bad premortem.
- **This is not the LLM Council.** The council gives multiple perspectives on a decision right now. The premortem sends Claude into the future where the decision already failed and works backward to explain why. Different psychological mechanism, different output. If the user seems to want multiple perspectives rather than failure analysis, suggest the council instead.
