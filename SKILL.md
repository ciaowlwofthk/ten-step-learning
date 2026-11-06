---
name: ten-step-learning
slug: ten-step-learning
displayName: ten-step-learning
display_name_en: ten-step-learning
version: 1.3.4
category: education
tags: [learning-methods, deep-research, knowledge-framework, feynman-technique, learning-roadmap]
summary: Say "ten-step learn X" to turn an unfamiliar topic into a checkable evidence chain — ten steps ending in a mobile-readable, printable single-file handbook; supports single-step calls and graceful degradation.
description: Use when the user wants to systematically learn, research or unpack an unfamiliar topic. Turns a topic into a ten-step verifiable evidence chain: fact-check, expert panel, contradiction adjudication, credibility scoring, resource roadmap, five-level ladder, 20-hour sprint, quiz, Feynman explanation, cheat sheet — delivered as a mobile-readable, printable single-file handbook. Supports single-step invocation and graceful degradation. Triggers: "ten-step learn X", "ten-step research X", "ten-step deconstruct X". Not for single-concept lookups or procedure queries. Skill id: ten-step-learning.
license: MIT
agent_created: true
---

# Ten-Step Method · Deep Learning Handbook Generator

## Why this skill

Most requests to "learn topic X systematically" end up as ten unrelated lists: a pile of concepts, a string of links, a few suggestions. After finishing, you still do not know which conclusions are trustworthy, which are marketing talk, or what to do next.

This skill turns learning into an **evidence chain**: first five perspectives collide with each other to expose disagreements; then evidence grading and credibility scoring push the noise down; finally everything lands on checkable actions. The ten steps depend on each other — you cannot drop the middle steps and keep only the beginning and the end.

## When to use it

Start when the user says any of the following:

- Explicit call: "ten-step learn XX", "ten-step research XX", "ten-step deconstruct XX"
- Equivalent descriptive request: asking for "multi-perspective expert analysis + contradiction list + briefing + credibility scoring + resource roadmap + learning ladder + sprint plan + quiz + Feynman explanation + cheat sheet" at once
- Single-step call: asking for only some steps, or with parameters for one step (e.g. "make the step-8 questions harder", "just do step 9, a Feynman explanation")

If the user says "ten-step method" but gives no topic, ask for the topic first — do not assume one.

## When not to use it

- The user just wants a definition or a short explanation: answer normally, do not start the ten-step flow.
- The user wants operating steps (how to install software, how to file taxes): that is procedural guidance, not a learning system.
- The topic is too narrow to support five perspectives (e.g. "the argument order of a certain function"): switch to targeted Q&A.
- The topic is too broad (e.g. "all of finance"): suggest a sub-topic, or a focus (e.g. "focus on evidence grading").

When it does not apply, explain the difference first, then offer two options — "answer directly" or "narrow the scope" — instead of forcing the flow and producing a half-finished artifact.

## Three-minute start

| Who you are | How to use it | What you get |
|:--|:--|:--|
| Entering a new field | Say "ten-step learn X", then answer and retell at steps 8 and 9 | An 11-section single-file HTML handbook, optionally exported to PDF |
| Checking whether it is worth it | Open the two real samples in `examples/` against the self-check list | A 30-second judgement |
| Wanting just one step | Say "only step X of the ten-step method, topic X" | That step's output plus a note on which prerequisites are missing |

**Minimal path**: give a topic → step 0 verifies facts online and confirms scope with you → steps 1–7 are delivered automatically → you answer at step 8 and retell at step 9 → you receive the cheat sheet and the full handbook. Only steps 8 and 9 need your input.

## Ten-step structure and hard requirements

The table has 11 rows: **step 0 is a gate** (no online verification, no writing), **steps 1–10 are the "ten steps"**.

| Step | Output | Hard requirement |
|:--|:--|:--|
| 0 · Fact check | Topic scope and verification record | For current rules, prices, lists or statutes, verify online first and record the date; never write from memory |
| 1 · Five-perspective panel | Statements from five kinds of experts | Each must give "position / 3 pieces of evidence / a hidden insight specific to that perspective"; a hidden insight is what that perspective knows but usually does not say |
| 2 · Contradiction list | Conflicts and adjudication | Four blocks: viewpoint conflicts (with conditional adjudication), evidence strength grading, points of consensus, industry blind spots |
| 3 · Concise briefing | 60-second script + 5 findings + 3 actions | Script 300–400 words, conversational; actions concrete enough to say "what to do this week" |
| 4 · Credibility scoring | Scored table | Score = evidence-type weight × freshness; below 80 mark "to verify" and name the exact missing data |
| 5 · Resources and roadmap | 5 resources + 7-day plan | Cover five categories: textbooks, official rules, practitioner books, free courses, hands-on tools; each day must produce something checkable |
| 6 · Five-level ladder | Cognition → rules → principles → strategy → practice | Each level has three items: passing criteria, pitfalls, self-test question |
| 7 · 20-hour sprint | 8 modules + 5–7 hands-on projects | Total exactly 20 hours; at least 1 observation-only project |
| 8 · Quiz | 10 four-choice questions | Increasing difficulty; every wrong option gets a diagnosis; never skip ahead when the user answers wrong |
| 9 · Feynman explanation | 12-year-old version + retelling check | Zero jargon, or explain jargon on the spot; include 1 diagram; end with 5–7 retelling criteria |
| 10 · Cheat sheet | One page | Sections for concepts, key metrics, viewpoint mapping, parameters, thresholds, risk red lines |

Full operating details, the five perspective definitions, scoring weights and quantitative metrics are in `references/execution-playbook.md`.

## How to use it

Say any of the following to the agent:

1. "Ten-step learn convertible bonds" — generate the full ten-step handbook as HTML.
2. "Ten-step research GLP-1 drugs, focus on evidence grading" — adjust the ten-step mix by focus (thicken steps 2 and 4, keep the rest).
3. "Ten-step deconstruct the Kubernetes scheduler, make step 8 harder" — single-step parameters are adjustable.

**Single-step rule**: explicitly say "only do step X"; produce that step to its hard requirement and state which prerequisites are missing and how that affects quality. **Interaction gates**: steps 8 and 9 must wait for the user's answers or retelling before continuing — do not complete them on the user's behalf; if skipped, state the loss first and mark the handbook "not accepted".

## Output specification

- Default to a **single-file HTML**: self-contained styles and inline graphics, no external dependencies, `max-width` controls the text column, readable on mobile; the CSS block from the samples in `examples/` can be reused directly.
- File name `<topic>-ten-step-handbook.html`, using a short topic name without spaces or punctuation, so the user can forward it directly.
- When a print version is needed, convert to PDF (use an HTML→PDF capability if the runtime provides one, e.g. the `html-to-pdf` skill; otherwise print from the browser), and deliver both; PDF is primary, HTML is easier to keep editing. For page-count verification, take the maximum of all `/Count` values (the first match is a nested node and gives a false reading).
- In print styles, avoid page breaks inside tables, cards and questions.
- Write in the user's language; prefer tables over long paragraphs; every factual number carries a source and verification date.
- The step-0 verification record **must** use three columns — conclusion / source / verification date — fully filled, for later review.

## Error handling and degradation

When something goes wrong, guide the user with a fixed script instead of quietly forcing content or giving up. Each scenario has an error code (E1–E5) so users can reference it directly:

| Code | Scenario | What to say (quotable) | Degradation |
|:--|:--|:--|:--|
| E1 | Offline / search unavailable | "Online search is unavailable, so step 0 cannot be verified. Option 1: offline edition — mark every current fact 'unverified' with a to-verify list. Option 2: wait until the network is back. Which one?" | Skip live verification; add an "unverified" banner to the cover; list what to check and where; drop the freshness coefficient one level |
| E2 | Insufficient sources / conflicting sources | "This conclusion is supported only by [source type], which is not strong evidence. Option 1: give a conditional conclusion with a confidence level. Option 2: narrow to a sub-topic with enough evidence. Which one?" | Write "holds under [conditions], confidence high/medium/low"; low confidence goes to "to verify"; never pad evidence |
| E3 | Generation interrupted | "The handbook stopped at step N; completed so far: [...]. Option 1: continue from the interruption (recommended). Option 2: deliver only the remaining steps. Which one?" | Before continuing, restate completed steps' key rulings and numbering to keep cross-references consistent; never silently rewrite from scratch |
| E4 | Topic unsuitable | "At step N the topic cannot support the full ten steps (reason: ...). Suggest [targeted Q&A / narrowing the topic]." | Stop instead of padding; mark delivered fragments "not a complete handbook" |
| E5 | PDF conversion failed | "PDF conversion failed (reason: ...); the HTML version is complete and usable. Ping me once a conversion capability is installed and I will finish the PDF." | Deliver HTML only |

**Retry policy (uniform rules)**:

- Search failures (E1): switch channels per the channel-degradation table and retry **at most once**; if it still fails, enter the degradation flow — do not retry endlessly.
- Conversion failures (E5): try a backup conversion channel **once**; if it still fails, deliver HTML only and do not rerun the same command repeatedly.
- Before any retry, tell the user "which step failed and how I plan to retry"; the user can stop it and choose degradation at any time.
- Treat every timeout as a failure and degrade; do not extend waits indefinitely. After a retry, keep the same error code (e.g. E1) for traceability.

**Channel degradation table** (switch channels level by level instead of getting stuck on one):

| Stage | Primary channel | Backup channel | Offline degradation |
|:--|:--|:--|:--|
| Online search (step 0 verification) | The agent's built-in web search | Another available search source, retried once (e.g. domain search, fetching an official page directly) | Mark "unverified" + to-verify list (E1) |
| Document conversion (HTML→PDF) | The runtime's HTML→PDF capability (e.g. the `html-to-pdf` skill) | Print to PDF from the local browser | Deliver HTML only (E5) |
| Page capture (when the topic needs live page data) | Browser automation capability (e.g. the `browser-pilot` skill) | Ask the user to export the page manually | Leave that data empty and mark it per E2 |

**General principle**: ask before degrading; never cut content on your own before the user chooses; degraded output must explicitly state what is missing; no exception justifies writing unverified content as a conclusion.

## Quality red lines

1. The ten steps must build on each other; never write them as ten parallel lists.
2. The "hidden insights" in step 1 must not be platitudes — they must be what that perspective knows but usually does not say.
3. Step 2's adjudication must state conditions ("who is right, under what premises"); no both-sides-are-right fudging.
4. Low scores in step 4 must name the missing data category; no empty phrases like "more research is needed".
5. Step 8 must not skip the explanation just because the user answered wrong.
6. Avoid absolutes; describe with probabilities and conditions — no "inevitable", "guaranteed profit", "certain".
7. For high-stakes domains such as investing, medicine or law, the deliverable must contain an explicit disclaimer.
8. Never present unverified prices, rules, lists or statutes as conclusions.
9. Never walk through steps 8 and 9 on the user's behalf without their response.
10. Never state investment conclusions as causal claims ("dollar-cost averaging always beats ...") without conditions and sample sources.

## FAQ

**Q1. How is this different from "research X for me"?** Ordinary research gives a list of conclusions; the ten-step method gives an evidence chain — expose disagreements first (1–2), push noise down (4), land on checkable actions (5–7) and acceptance (8–9). The chain lets you judge whether the next new conclusion deserves trust.

**Q2. How long does it take? Can I skip steps?** Usually one long conversation (tens of minutes, depending on the topic). The steps form a dependency chain; removing middle steps breaks it. If you want only some steps, say "only step X" and the output will state what is missing.

**Q3. Why must step 0 verify online first?** "Current facts" — rules, prices, lists, statutes — are necessarily stale in training data; writing from memory produces wrong deliverables. Record conclusion / source / date for review.

**Q4. What if the topic is too small or too large?** Too small (cannot support five perspectives) → suggest targeted Q&A; too large → suggest a sub-topic or a focus. If it turns out unsuitable mid-way, stop and say so instead of padding.

**Q5. What happens if I answer wrong? Can I skip steps 8 and 9?** Wrong answers are not skipped — first explain "why you thought so and where it went wrong". You can skip, but the loss is stated first and the handbook is marked "not accepted".

**Q6. Is the output only HTML?** Default is a single-file HTML (mobile-readable, forwardable, printable); for print, produce a PDF with an HTML→PDF capability (e.g. the `html-to-pdf` skill). Word is out of default scope.

**Q7. Can it handle finance, medicine or law?** Yes — and such topics need it more — but deliverables carry a disclaimer and red lines forbid causal claims; conclusions carry conditions and sample sources; actual decisions follow official rules and licensed professionals.

**Q8. What happens when offline or short of sources?** Follow "Error handling and degradation": choose between an offline edition (current facts marked "unverified" + to-verify list) and waiting; degraded output is explicitly marked and never presents unverified content as conclusions.

## Sample outputs

`examples/` contains two real generated samples covering different topics, ready to open and compare:

- `sample-index-fund-handbook.html` — "Index Fund Investing · Ten-Step Handbook" (finance): all 11 sections, with a filled verification table (conclusion / source / date), 5 hands-on projects (including 1 observation-only), an inline SVG diagram, a scoring table and quiz items with wrong-option diagnoses. Step 8 keeps only 2 questions to control size (a full run produces 10); this is noted inside the file.
- `sample-sleep-memory-compact.html` — "Sleep and Memory Consolidation · Ten-Step Compact Handbook" (cognitive science, compact complete edition): the same 11-section structure with a non-finance topic, about one third the length, proving the skill is topic-agnostic.
- `README.md` — copyable prompts, output specs, and the quality bar the samples deliberately meet (use it to check whether an output is acceptable).

## Requirements and environment

- **Required**: an agent runtime with web search. Step 0's verification depends on live search; a fully offline environment lowers credibility significantly — follow "Error handling and degradation" and mark the "unverified" scope in the deliverable.
- **Optional**: an HTML→PDF capability (e.g. the `html-to-pdf` skill installed locally) for a PDF; without it, degrade to HTML only — the main flow is unaffected.

## Working with external capabilities

Use the following capabilities as the runtime actually provides them; when one is missing, follow "Error handling and degradation" instead of pretending it is available:

- Output to PDF → HTML→PDF conversion (e.g. the `html-to-pdf` skill, or browser printing)
- Login-only pages or dynamic content → browser automation (e.g. the `browser-pilot` skill, or ask the user to export manually)
- A-share quotes or individual stock prices → fetch live data before writing; never write prices from memory
- Financial data retrieval → market/financial data capability (e.g. a data skill or API)

## Disclaimer

Content produced by this skill is a learning framework and information organization, not investment, medical, legal or other professional advice. For specific decisions, follow official rules and licensed professionals.
