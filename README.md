# Ten-Step Learning · Deep-Learning Handbook Generator

![Version](https://img.shields.io/badge/version-1.3.4-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Format](https://img.shields.io/badge/format-SKILL.md-8A2BE2)

Turns "teach me X systematically" from **ten unrelated checklists** into **one auditable chain of evidence**, delivered as a single-file HTML handbook you can read on a phone and print on paper.

> A **SKILL.md**-native agent skill — no scripts, no external dependencies. Works with WorkBuddy, Claude Code and any runtime that follows the Agent Skills convention. Triggers: "ten-step learn X", "ten-step research X".

---

## Why this skill exists

Most "learn X systematically" requests end up as a pile of concepts, a list of links, and a few opinions. You finish and still cannot answer: **which conclusions are trustworthy, which are marketing, and what do I do next?**

This skill turns learning into an evidence chain. Five opposing perspectives are pitted against each other first, so disagreements surface instead of being smoothed over. Evidence grading and credibility scores then suppress the noise. Everything lands on actions you can check. The ten steps depend on one another — you cannot delete the middle and keep only the intro and the summary.

## The ten steps

| Step | Output | Hard requirement |
|:--|:--|:--|
| 0 · Fact-check gate | Topic boundary + verification log | Anything involving current rules, prices, lists or statute text must be verified online with the date recorded. Never written from memory. |
| 1 · Five-perspective panel | Statements from five expert types | Each must supply "position / 3 pieces of evidence / one insider detail" |
| 2 · Contradiction list | Conflicts + adjudication | All four blocks required: conflicts (with conditional rulings), evidence-strength grading, consensus points, industry blind spots |
| 3 · Condensed brief | 60-second script + 5 findings + 3 actions | Script 300–400 words, spoken register; actions concrete enough to answer "what do I do this week" |
| 4 · Credibility scoring | Table with scores | Score = evidence-type weight × freshness. Below 80 is labelled "unverified" with the missing data named. |
| 5 · Resources and roadmap | 5 resources + 7-day route | Covers all five categories: textbook, official rules, practitioner monograph, free course, hands-on tool |
| 6 · Five-level ladder | Awareness → rules → principles → strategy → practice | Each level carries three items: pass criteria, common traps, self-test question |
| 7 · 20-hour sprint | 8 modules + 5–7 projects | Durations sum to exactly 20 hours; at least one observational project |
| 8 · Quiz | 10 four-option questions | Increasing difficulty; every distractor carries a diagnosis; wrong answers do not skip ahead |
| 9 · Feynman explanation | 12-year-old version + recall test | Zero jargon, or jargon explained on the spot; one diagram; recall criteria at the end |
| 10 · Cheat sheet | One page | Concepts, key metrics, position map, parameters, thresholds and risk red lines in separate zones |

Full operating detail — five-perspective definitions, scoring weights, quantitative metrics — is in [`references/execution-playbook.md`](references/execution-playbook.md).

## Quick start

### Install

Drop the repository into your agent's skills directory. **Keep the directory name `ten-step-learning`.**

| Runtime | Skills directory |
|:--|:--|
| WorkBuddy | `~/.workbuddy/skills/ten-step-learning` |
| Claude Code | `~/.claude/skills/ten-step-learning` |
| Other SKILL.md-compatible runtimes | Their configured skills directory, subfolder named `ten-step-learning` |

```bash
git clone https://github.com/ciaowlwofthk/ten-step-learning.git ~/.workbuddy/skills/ten-step-learning
```

Windows (PowerShell):

```powershell
git clone https://github.com/ciaowlwofthk/ten-step-learning.git "$env:USERPROFILE\.workbuddy\skills\ten-step-learning"
```

No git? Download `ten-step-learning-1.3.4-en.zip` from [Releases](https://github.com/ciaowlwofthk/ten-step-learning/releases), unzip into the directory from the table above, and confirm `SKILL.md` sits at the root of that directory.

Agent with no skill mechanism? Load the full text of `SKILL.md` as a system prompt or rules file — the effect is the same.

### Use it

Say any one of these to your agent:

- "Take me through convertible bonds with the ten-step method" — generates the full handbook
- "Ten-step research on GLP-1 drugs, weight the evidence grading more heavily" — adjusts the emphasis
- "Ten-step breakdown of the Kubernetes scheduler, make step 8 harder" — per-step parameters are tunable
- "Only step 8, topic X" — single-step invocation, still bound by that step's hard requirements

**Shortest path:** give a topic → step 0 verifies online and hands you the boundary for confirmation → steps 1–7 are delivered automatically → you answer step 8 and recall step 9 → you receive the cheat sheet and the full handbook. You only lift a finger at steps 8 and 9.

## What the output looks like

`examples/` holds two **really generated** samples you can open side by side:

| File | Topic | What to look at |
|:--|:--|:--|
| [`sample-index-fund-handbook.html`](examples/sample-index-fund-handbook.html) | Index-fund dollar-cost averaging (finance) | All 11 sections, a filled-in verification log, 5 hands-on projects, inline SVG diagrams, quiz items with distractor diagnoses |
| [`sample-sleep-memory-compact.html`](examples/sample-sleep-memory-compact.html) | Sleep and memory consolidation (cognitive science) | Same structure on a non-financial topic, about a third the length — proof the skill is topic-agnostic |

Output spec: one HTML file, self-contained styling, no external dependencies, readable on mobile, named `<topic>-ten-step-handbook.html`. Add a PDF when a print edition is needed and both are delivered together. Quality criteria: [`examples/README.md`](examples/README.md).

> Both samples were originally generated in Chinese and translated for this English edition. The numbers inside are illustrative, not investment or medical advice.

## Repository structure

```text
ten-step-learning/
├─ SKILL.md                        # Main file: routing, ten-step hard requirements, degradation, red lines
├─ references/
│  └─ execution-playbook.md        # Operating detail: per-step actions, five perspectives, weights, pre-delivery check
├─ examples/                       # Two real sample outputs + quality comparison notes
├─ workbuddy.json                  # Optional metadata (bilingual descriptions); other runtimes ignore it
└─ LICENSE.md
```

## Requirements and environment

- **Required:** an agent runtime with live web search. Step 0's fact-check depends on it; a fully offline environment degrades to "unverified + to-verify list" mode.
- **Optional:** with a local HTML→PDF capability installed, a PDF is produced as well. Without it you still get the HTML; the main flow is unaffected.

## Scope and boundaries

Out-of-scope requests are handled by stating the difference and offering two options — answer directly, or narrow the scope — rather than forcing the pipeline:

- You want a definition or a short explanation → ordinary answer
- You want operating steps (how to install software, how to file taxes) → process guidance, not a learning system
- The topic is too narrow to support five perspectives (e.g. "argument order of one function") → targeted Q&A
- The topic is too broad (e.g. "all of finance") → split into sub-topics or pick an angle

For investment, medical or legal topics the deliverable carries an explicit disclaimer, and every conclusion ships with its conditions of validity and sample provenance.

## Design notes

- **Evidence chain over checklist.** The ten steps must progress. Step 2's adjudication must state conditions ("under what premise is each side right") — no fence-sitting.
- **Auditable.** Every number and date must point to the verification log or a source. What cannot be pointed to gets deleted or marked "illustrative".
- **Degradable.** Offline, thin sources, interrupted generation and PDF failure all have numbered codes (E1–E5) and fixed wording. Ask first, then degrade.
- **Interaction gates.** Steps 8 and 9 wait for your answer and your recall. The agent will not complete them for you; skipping requires stating the loss and tagging the output "unreviewed".

## Compatibility

- Skill format: `SKILL.md` (YAML frontmatter + Markdown body) following the Agent Skills convention. Usable as-is by WorkBuddy, Claude Code and compatible runtimes.
- The body never binds itself to one runtime's proprietary tools: PDF conversion, page capture and data retrieval are described as *capabilities* with example skill names. Anything missing degrades per E1–E5 instead of pretending to work.
- `workbuddy.json` is optional WorkBuddy metadata; ignore it elsewhere.
- No scripts, no external dependencies. Network access is used only for step 0.

## License

[MIT](LICENSE.md) © 2026 ten-step-learning contributors
